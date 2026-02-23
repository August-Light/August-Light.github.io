# 预处理

## 标准化 & 归一化

标准化：

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)
print(X_scaled)
```

归一化：

```python
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()
X_scaled = scaler.fit_transform(X)
print(X_scaled)
```

## 缺失值

查看每列缺失值数量：

```python
print(df.isnull().sum())
```

删除缺失值：

```python
df_clean = df.dropna()
```

填充缺失值：

```python
from sklearn.impute import SimpleImputer

imputer = SimpleImputer(strategy='mean')
X = imputer.fit_transform(X)
```

TODO:

# 数据集分割

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)
```

`test_size` 表示测试集大小和总的数据集大小的比值，比如 `test_size=0.3` 表示从数据集选取 $30\%$ 作为测试集。

`randon_state` 是随机数种子。

# 编码

## 标签

TODO:

## 独热

```python
from sklearn.preprocessing import OneHotEncoder

X = [
    ["本科", "男"],
    ["硕士", "女"],
    ["博士", "女"],
]

encoder = OneHotEncoder(sparse_output=False)
X_encoded = encoder.fit_transform(X)
print(X_encoded)
```

Output:

```
[[0. 1. 0. 0. 1.]
 [0. 0. 1. 1. 0.]
 [1. 0. 0. 1. 0.]]
```

解释：

|  | 0 | 1 | 2 |
| - | - | - | - |
| 本科 |  | 1 |  |
| 硕士 |  |  | 1 |
| 博士 | 1 |  |  |

|  | 0 | 1 |
| - | - | - |
| 男 |  | 1 |
| 女 | 1 |  |

分别编码，直接拼接。

# 训练

TODO:

```python
from sklearn.linear_model import LogisticRegression

model = LogisticRegression()
model.fit(X_train, y_train)
```

# 评估

## MSE

```python
from sklearn.metrics import mean_squared_error

mse = mean_squared_error(y_test, y_pred)
```

## 混淆矩阵相关的指标

```python
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score

accuracy = accuracy_score(y_test, y_pred)
precision = precision_score(y_test, y_pred)
recall = recall_score(y_test, y_pred)
f1 = f1_score(y_test, y_pred)
```

# Pipeline

```python
from sklearn.pipeline import Pipeline

pipeline = Pipeline([
    ("scaler", StandardScaler()),
    ("linear", LinearRegression())
])
pipeline.fit(X_train, y_train)
y_pred = pipeline.predict(X_test)
```

`Pipeline` 初始化时，每一个二元组的第一个元素都是这一步的名字，可以自己乱起。