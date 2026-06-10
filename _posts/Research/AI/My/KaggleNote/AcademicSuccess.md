- [Problem](https://www.kaggle.com/competitions/playground-series-s4e6/)
- [Dataset Description](https://archive.ics.uci.edu/dataset/697/predict+students+dropout+and+academic+success)

---

- 检查数据
  - 输入有序数特征和类型特征。手动标一下（有点累）。
  - 输出只有 $3$ 种：`Dropout`、`Enrolled`、`Graduate`。
  - 无缺失值。
- 最简单地，考虑使用 `sklearn` 的 `RandomForestClassifier`。
  - 代码笔记：`OneHotEncoder` 中参数 `handle_unknown='ignore'` 可以防止 test 遇到 train 没有的 category 时报错。
- 随机森林直接拿下 Private 榜 $0.82859$。暂时收工。
  - 接下来可能要做的：K-fold 验证、随机森林调参、更换树模型