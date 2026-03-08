# 预处理

## 标准化 & 归一化

标准化：

```py
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)
print(X_scaled)
```

归一化：

```py
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()
X_scaled = scaler.fit_transform(X)
print(X_scaled)
```

## 缺失值

查看每列缺失值数量：

```py
print(df.isnull().sum())
```

删除包含缺失值的行：

```py
df_clean = df.dropna()
```

填充缺失值：

```py
from sklearn.impute import SimpleImputer

imputer = SimpleImputer(strategy='mean')
X = imputer.fit_transform(X)
```

`strategy` 可以选择：
- `mean`
- `median`
- `most_frequent`

# 数据集分割

```py
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.3, random_state=42
)
```

`test_size` 表示测试集大小和总的数据集大小的比值，比如 `test_size=0.3` 表示从数据集选取 $30\%$ 作为测试集。

`randon_state` 是随机数种子。

# 编码

## 标签

```py
from sklearn.preprocessing import LabelEncoder

X = ["red", "green", "blue", "green", "red"]

encoder = LabelEncoder()
X_encoded = encoder.fit_transform(X)
print(X_encoded) # [2 1 0 1 2]
```

只能处理一维数据！

## 独热 (Pandas)

```py
import pandas as pd

df = pd.DataFrame({
    'color': ['red', 'green', 'blue', 'green', 'red'],
    'size': ['S', 'M', 'L', 'M', 'S'],
    'price': [10, 20, 15, 25, 30]
})

df_encoded_auto = pd.get_dummies(df)
print(df_encoded_auto)
```

Output:

```
   price  color_blue  color_green  color_red  size_L  size_M  size_S
0     10       False        False       True   False   False    True
1     20       False         True      False   False    True   False
2     15        True        False      False    True   False   False
3     25       False         True      False   False    True   False
4     30       False        False       True   False   False    True
```

可以指定 `columns`，若不指定就是自动对所有非数值作独热编码。

## 独热 (Sklearn)

```py
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

- `sklearn.linear_model`
  - `LinearRegression`
  - `LogisticRegression`
  - `Lasso`
  - `Ridge`
- `sklearn.neighbors`
  - `KNeighborsClassifier`
- `sklearn.svm`
  - `SVC` / `SVR`
- `sklearn.tree`
  - `DecisionTreeClassifier` / `DecisionTreeRegressor`
- `sklearn.cluster`
  - `KMeans`

以 `LinearRegression` 为例：

```py
from sklearn.linear_model import LinearRegression

model = LinearRegression()
model.fit(X_train, y_train)
y_pred = model.predict(X_test)

print(y_pred, y_test)
```

一个完整可以跑的：

```py
import numpy as np
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import r2_score

np.random.seed(42)

X = np.array([[1], [2], [3], [4], [5], [6], [7], [8], [9], [10]])
y = 2 * X.flatten() + 1 + np.random.randn(10) * 2

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.3, random_state=42
)

model = LinearRegression()
model.fit(X_train, y_train)
y_pred = model.predict(X_test)

print(y_pred, y_test)
print(r2_score(y_test, y_pred))
```

# 评估

## MSE & $R^2$

```py
from sklearn.metrics import mean_squared_error, r2_score

mse = mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)
```

## 混淆矩阵相关的指标

```py
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score

accuracy = accuracy_score(y_test, y_pred)
precision = precision_score(y_test, y_pred)
recall = recall_score(y_test, y_pred)
f1 = f1_score(y_test, y_pred)
```

# Pipeline

```py
from sklearn.pipeline import Pipeline

pipeline = Pipeline([
    ("scaler", StandardScaler()),
    ("linear", LinearRegression())
])
pipeline.fit(X_train, y_train)
y_pred = pipeline.predict(X_test)
```

`Pipeline` 初始化时，每一个二元组的第一个元素都是这一步的名字，可以自己乱起。