# BERT (Bidirectional Encoder Representations from Transformers)

https://d2l.ai/chapter_natural-language-processing-pretraining/bert.html

<img src="https://d2l.ai/_images/elmo-gpt-bert.svg" width=400/>

<img src="https://d2l.ai/_images/bert-input.svg" width=500/>

## Masked Language Modeling

- 选中 $15\%$ 作 mask
  - $80\%$ `<mask>`
  - $10\%$ 随机交换

# Example: 组合词分割问题（Attention）

数据量很大

跑通 Baseline 发现 $0$ 分，观察输出发现巨小，因此预测全部为 $0$。

加入 Attention：

```py
import torch
from torch import nn

MAX_LEN = 128 # 单个词的最大长度

class MyModel(nn.Module):
    def __init__(self, vocab_size, embedding_dim=256, num_heads=8, num_layers=3, ffn_dim=512, dropout=0.2):
        super().__init__()
        self.embedding = nn.Embedding(vocab_size + 1, embedding_dim, padding_idx=0)
        self.pos_encoding = nn.Embedding(MAX_LEN, embedding_dim)
        self.emb_dropout = nn.Dropout(dropout)

        encoder_layer = nn.TransformerEncoderLayer(
            d_model=embedding_dim,
            nhead=num_heads,
            dim_feedforward=ffn_dim,
            dropout=dropout,
            activation="gelu",
            batch_first=True,
            norm_first=True
        )
        self.transformer = nn.TransformerEncoder(encoder_layer, num_layers=num_layers)
        self.mlp = nn.Sequential(
            nn.Linear(embedding_dim, embedding_dim // 2),
            nn.GELU(),
            nn.Dropout(dropout),
            nn.Linear(embedding_dim // 2, 1),
            nn.Sigmoid()
        )

    def forward(self, x):
        # x: (batch_size, seq_len)
        positions = torch.arange(x.size(1), device=x.device).unsqueeze(0)
        emb = self.embedding(x) + self.pos_encoding(positions)
        emb = self.emb_dropout(emb)

        pad_mask = (x == 0)

        enc_out = self.transformer(emb, src_key_padding_mask=pad_mask)
        logits = self.mlp(enc_out).squeeze(-1)
        return logits
```

TODO:

