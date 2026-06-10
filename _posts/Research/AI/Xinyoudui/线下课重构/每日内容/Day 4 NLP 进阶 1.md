# NLP

$$\text{text} \xrightarrow{\text{tokenize}} \text{token ids} \xrightarrow{\text{Embedding}} \text{vectors} \xrightarrow{\textcolor{#CF1020}{\text{RNN}}} \text{output}$$

# Tokenize



# Embedding

```py
nn.Embedding(num_embeddings, embedding_dim)
```

把这 `num_embeddings` 个 token 的每一个映射到一个维数为 `embedding_dim` 的向量。

对于 token $i$，取出系数矩阵的第 $i$ 行。

$$x_i = \text{Embedding}(\text{token}_i)$$

此时获得

# RNN

```py
nn.RNN(input_size, hidden_size, batch_first=True)
```

`batch_first` 默认值为 `False`，改成 `True` 是为了和 `DataLoader` 的输出格式一致。

