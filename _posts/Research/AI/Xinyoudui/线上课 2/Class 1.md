- 要 drop 掉 `id`
- 思考：数据的类型？
  - 可比较的数值
  - 不可比较的数值 / 字符串，表示类型
  - 暗含可比较关系的字符串
  - 对预测无意义的特征
- `train_test_split` 可以 `stratify`
  - 分出的测试集变量名可以改成 `val`。
- `xgboost` 有 `XGBClassifier`
- 喜欢的话，可以使用 `SimpleNamespace` 保存全局变量
- Stacking 可以先找一堆模型做预测，再用预测值当成 feature 再做一次预测。

# Pandas

- `.info` 每列信息
- `.corr` （数值的）相关系数矩阵
  - `seaborn.heatmap` 热力图