# NLP

https://d2l.ai/chapter_recurrent-neural-networks/index.html

https://d2l.ai/chapter_recurrent-modern/index.html

## Tokenize

TODO:

## RNN (Recurrent Neural Network, 循环神经网络)

[Link](https://d2l.ai/chapter_recurrent-neural-networks/rnn.html)

普通的神经网络认为输入之间不依赖。但是对于语言处理我们需要记住前面的句子在说什么。因此我们需要一个这样的“前缀和”结构：

$$\textcolor{#1E90FF}{h_t} = f(\textcolor{#E32636}{x_t}, \textcolor{#1E90FF}{h_{t-1}})$$

$h$ 被称为 **hidden state (隐藏变量 / 隐状态)**。具体来说：

- input 为红色
- hidden state 为蓝色
- output 为绿色

(1) 隐藏变量这样传递：

$$\textcolor{#1E90FF}{H_t} = \phi(\textcolor{#E32636}{X_t} W_{\text{xh}} + \textcolor{#1E90FF}{H_{t-1}} W_{\text{hh}} + b_{\text{h}})$$

(2) 每层的输出：

$$\textcolor{#03C03C}{O_t} = \textcolor{#1E90FF}{H_t} W_{\text{hq}} + b_{\text{q}}$$

<img src="https://d2l.ai/_images/rnn.svg" width=500/>

我们可以使用这样的模型，根据文字序列中前面的 token 去预测下一个 token：

<img src="https://d2l.ai/_images/rnn-train.svg" width=500/>

## LSTM (Long Short-Term Memory)

https://d2l.ai/chapter_recurrent-modern/lstm.html

RNN 无法处理长序列文本

TODO:

- **Forget Gate**
- **Input Gate**
- **Output Gate**

## GRU

https://d2l.ai/chapter_recurrent-modern/gru.html

- Gate
  - **Update Gate**
  - **Reset Gate**
- Candidate Hidden State

TODO:

## Deep RNN

TODO:

## Bidirectional RNN

https://d2l.ai/chapter_recurrent-modern/bi-rnn.html

TODO:

## Encoder–Decoder Architecture

https://d2l.ai/chapter_recurrent-modern/encoder-decoder.html

<img src="https://d2l.ai/_images/encoder-decoder.svg" width=400/>

ChatGPT 说的：

$$\text{Sequence} \xrightarrow{\text{Encoder}} \text{Vector} \xrightarrow{\text{Decoder}} \text{Sequence}$$

TODO:

## Seq2Seq

<img src="https://d2l.ai/_images/seq2seq.svg" width=500/>

<img src="https://d2l.ai/_images/seq2seq-details.svg" width=300/>

TODO:

### 预测序列的评估：BLEU (Bilingual Evaluation Understudy)

https://d2l.ai/chapter_recurrent-modern/seq2seq.html#evaluation-of-predicted-sequences