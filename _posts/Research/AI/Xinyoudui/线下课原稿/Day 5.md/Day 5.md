# Example: 新闻文本分类任务（LSTM）

TODO:

```py
class LSTMClassifier(nn.Module):
    def __init__(self, vocab_size, embedding_dim, hidden_dim, num_classes, pad_idx):
        super(LSTMClassifier, self).__init__()
        self.embedding = nn.Embedding(
            vocab_size, embedding_dim, padding_idx=pad_idx)
        self.lstm = nn.LSTM(embedding_dim, hidden_dim,
                            batch_first=True, bidirectional=True)
        self.dropout = nn.Dropout(0.2)
        self.ln = nn.LayerNorm(2 * hidden_dim)
        self.fc = nn.Linear(2 * hidden_dim, num_classes)

    def forward(self, x):
        embedded = self.embedding(x)
        lstm_output, (hidden, cell) = self.lstm(embedded)
        last_hidden = torch.cat((hidden[-2], hidden[-1]), dim=1)
        last_hidden = self.ln(self.dropout(last_hidden))
        logits = self.fc(last_hidden)
        return logits
```

# Attention

**Attention is all you need!**

## QKV

https://d2l.ai/chapter_attention-mechanisms-and-transformers/queries-keys-values.html

ChatGPT：

Query (Q)：你要查询的内容 → 用来问“我关注的东西和谁相关？”

Key (K)：序列中每个元素的“标签” → 用来回答“我是谁/我有什么特征？”

Value (V)：序列中每个元素的实际信息 → 用来“提供给你内容”。

## Attention Scoring Functions

对于一个 query $q$，其 attention 为：

$$\text{Attention}(q) = \sum_i \frac {\alpha(q, k_i)} {\sum_j \alpha(q, k_j)} v_i$$

（这样保证了所有权值和为 $1$）

<img src="https://d2l.ai/_images/qkv.svg" width=350/>

若 $\alpha$ 含有 $\exp$ 结构，令 $a = \ln \alpha$：

$$\text{Attention}(q) = \sum_i \frac {\exp a(q, k_i)} {\sum_j \exp a(q, k_j)} v_i$$

这就可以看作是对于 $a$ 的 softmax 操作。

### Masked Softmax

https://d2l.ai/chapter_attention-mechanisms-and-transformers/attention-pooling.html

TODO:

https://d2l.ai/chapter_attention-mechanisms-and-transformers/attention-scoring-functions.html

### Scaled Dot Product Attention (缩放点积注意力)

考虑高斯核

$$\begin{aligned}
   a(q,k) =& - \frac 1 2 \lVert q - k \rVert^2 \\
    =& q^T k - \frac 1 2 \left( \lVert q \rVert^2 + \lVert k \rVert^2 \right) \\
\end{aligned}$$

记住我们是一个 softmax，因此常数可以忽略：

$$a(q,k) = q^T k - \frac 1 2 \lVert k \rVert^2$$

与此同时，在标准化（`LayerNorm`）后 $q,k$ 的每个维度都均值为 $0$ 方差为 $1$。$\lVert k \rVert$ 往往变化不大，因此也忽略 $\lVert k \rVert^2$。令维度为 $d$，就有：

$$a(q,k) = q^T k$$

$$\begin{aligned}
    \text{Var}(q^T k) &= d \\
    \text{Var}\left( \frac {q^T k} {\sqrt d} \right) &= 1 \\
\end{aligned}$$

Scaled dot product attention 的 scaled 指的就是除以 $\sqrt d$。

因此我们令

$$a(q, k) = \frac {q^T k} {\sqrt d}$$

$$\boxed{
    \text{Attention}(q) = \sum_i \text{softmax}\left( \frac {q^T k_i} {\sqrt d} \right) v_i
}$$

<img src="https://d2l.ai/_images/attention-output.svg" width=450/>

打包成矩阵：

$$\text{softmax}\left( \frac {\mathbf Q \mathbf K^T} {\sqrt d} \right) \mathbf V$$

## Multi-Head Attention

https://d2l.ai/chapter_attention-mechanisms-and-transformers/multihead-attention.html

有时我们想同时利用好几个 Attention 模型，怎么办？如图：

<img src="https://d2l.ai/_images/multi-head-attention.svg" width=400/>

这被称为 Multi-head attention。

## Self-Attention

https://d2l.ai/chapter_attention-mechanisms-and-transformers/self-attention-and-positional-encoding.html

## 比较 CNN、RNN 与 Self-Attention

<img src="https://d2l.ai/_images/cnn-rnn-self-attention.svg" width=300/>

## Positional Encoding

$\sin, \cos$。很经典。但现在一般不用，用的都是 rope

每个时刻不同

（当然考的概率很小）

## The Transformer Architecture

https://d2l.ai/chapter_attention-mechanisms-and-transformers/transformer.html

<img src="https://d2l.ai/_images/transformer.svg" width=500/>

add & norm，是残差。

# 手撕 Multi-Head Attention！

虽然写代码的时候不需要自己写，但是万一填空题考了呢？

```py
from math import sqrt
import torch
from torch import nn


def masked_softmax(X, valid_lens):
    # https://d2l.ai/chapter_attention-mechanisms-and-transformers/attention-scoring-functions.html#masked-softmax-operation
    if valid_lens is None:
        return nn.functional.softmax(X, dim=-1)
    else:
        shape = X.shape
        if valid_lens.dim() == 1:
            valid_lens = torch.repeat_interleave(valid_lens, shape[1])
        else:
            valid_lens = valid_lens.reshape(-1)
        X = X.reshape(-1, shape[-1])
        maxlen = X.size(1)
        mask = torch.arange(maxlen, dtype=torch.float32, device=X.device)[
            None, :] < valid_lens[:, None]
        X[~mask] = -1e6  # -inf
        return nn.functional.softmax(X.reshape(shape), dim=-1)


class MultiHeadAttention(nn.Module):
    # https://d2l.ai/chapter_attention-mechanisms-and-transformers/multihead-attention.html#implementation
    def __init__(self, key_size, query_size, value_size, num_hiddens, num_heads, dropout, bias=False, **kwargs):
        super().__init__()
        self.num_heads = num_heads
        self.W_q = nn.Linear(query_size, num_hiddens, bias=bias)
        self.W_k = nn.Linear(key_size, num_hiddens, bias=bias)
        self.W_v = nn.Linear(value_size, num_hiddens, bias=bias)
        self.W_o = nn.Linear(num_hiddens, num_hiddens, bias=bias)
        self.dropout = nn.Dropout(dropout)

    def transpose_qkv(self, X):
        X = X.reshape(X.shape[0], X.shape[1], self.num_heads, -1)
        X = X.permute(0, 2, 1, 3)
        return X.reshape(-1, X.shape[2], X.shape[3])

    def transpose_output(self, X):
        X = X.reshape(-1, self.num_heads, X.shape[1], X.shape[2])
        X = X.permute(0, 2, 1, 3)
        return X.reshape(X.shape[0], X.shape[1], -1)

    def forward(self, queries, keys, values, valid_lens):
        queries = self.transpose_qkv(self.W_q(queries))
        keys = self.transpose_qkv(self.W_k(keys))
        values = self.transpose_qkv(self.W_v(values))

        if valid_lens is not None:
            valid_lens = torch.repeat_interleave(
                valid_lens, repeats=self.num_heads, dim=0)

        d = queries.shape[-1]
        scores = torch.bmm(queries, keys.transpose(1, 2) / sqrt(d))
        self.attention_weights = masked_softmax(scores, valid_lens)
        output = torch.bmm(self.dropout(self.attention_weights), values)
        output_concat = self.transpose_output(output)
        output = self.W_o(output_concat)
        return output


input_dim, num_hiddens, num_heads = 256, 100, 5
attention = MultiHeadAttention(
    input_dim, input_dim, input_dim, num_hiddens, num_heads, 0.5)
attention.eval()

batch_size, num_queries = 2, 4
num_kvpairs, valid_lens = 6, torch.tensor([3, 2])
X = torch.ones((batch_size, num_queries, input_dim))
Y = torch.ones((batch_size, num_kvpairs, input_dim))

print(attention(X, Y, Y, valid_lens).shape)
```

# Example: 化学动力学问题

> 化学家发现在一个反应中，$\ce{L2M}$ 的浓度降低速率与 $\ce{D}$ 的浓度成正比，与 $\ce{L}$ 的浓度成反比。
>
> 具体来说，这个反应长这样：
>
> $$\begin{cases}
>     \ce{L2M <=> LM + L} \\
>     \ce{LM + D -> LMD} \\
>     \ce{LMD + L <=> L2MD} \\
>     \ce{LM -> LMs} \\
>     \ce{LMs + L <=> L2Ms} \\
> \end{cases}$$
>
> 可写出动力学方程：
>
> $$\begin{cases}
>     r_{1+} = k_{1+} \times c(\ce{L2M}) \\
>     r_{1-} = k_{1-} \times c(\ce{LM}) \times c(\ce{L}) \\
>     \vdots \\
> \end{cases}$$
>
> 用差分方程刻画：
>
> $$\begin{cases}
>     \frac {\Delta c(\ce{L2M})} {\Delta t} = - r_{1+} + r_{1-} \\
>     \vdots \\
> \end{cases}$$
>
> 已知 $c(\ce{L2M}), c(\ce{D}), c(\ce{L})$ 在 $t = 0$ 时的值，求 $\ce{L2M}$ 的半衰期 $t_{1/2}$。

## 增加特征

题目说了这个很重要：

$$\frac {c(\ce{D})} {c(\ce{L})}$$

## 取对数

对于简单的微分方程：

$$\frac {dA} {dt} = -k A \implies A(t) = A(0) e^{-kt}$$

代入半衰期：

$$A(t_{1/2}) = A(0) e^{-k t_{1/2}} = \frac {A(0)} 2 \implies t_{1/2} = \frac {\ln 2} k$$

如果取对数，则可以变为线性的形式：

$$\boxed{
    \ln t_{1/2} = \ln \ln 2 - \ln k
}$$

## 可以考虑的方法

- `nn.Linear`
- `nn.Dropout`
- `nn.BatchNorm2d`
- 残差 `self.act(self.block(x) + x)`