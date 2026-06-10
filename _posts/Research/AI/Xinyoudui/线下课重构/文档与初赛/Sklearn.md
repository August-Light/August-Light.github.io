# Preprocessing

## 缺失值

```py
import numpy as np
import pandas as pd
from sklearn.impute import SimpleImputer

df = pd.DataFrame({
    "Name": ["Alice", "Bob", "Charlie", "Daniel"],
    "Age": [10, 25, np.nan, 30],
    "City": ["Shanghai", "Tokyo", "Beijing", "New York"],
})

print(df)

# 查看每列缺失值数量
print(df.isnull().sum())

# 删除包含缺失值的行
df_dropped = df.dropna()
print("df_dropped:")
print(df_dropped)

# 用均值填充缺失值
df_filled = df.copy()
columns = ["Age"]
imputer = SimpleImputer(strategy='mean')
df_filled[columns] = imputer.fit_transform(df[columns])
print("df_filled")
print(df_filled)
```

`strategy` 可以选择：
- `mean`
- `median`
- `most_frequent`

## 异常值

用 Pandas 去除超出上下界的异常值：

```py
import pandas as pd

df = pd.DataFrame({
    'A': [1, 2, 5, 100, 6, 8, -50, 6],
})

lower_bound, upper_bound = 0, 10
df = df[(df['A'] >= lower_bound) & (df['A'] <= upper_bound)]
print(df)

"""
   A
0  1
1  2
2  5
4  6
5  8
7  6
"""
```

## 数据集分割

```py
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.3, random_state=42
)
```

- `test_size` 表示测试集大小和总的数据集大小的比值，比如 `test_size=0.3` 表示从数据集选取 $30\%$ 作为测试集。
- `randon_state` 是随机数种子。

## 编码

### 标签

```py
from sklearn.preprocessing import LabelEncoder

X = ["red", "green", "blue", "green", "red"]

encoder = LabelEncoder()
X_encoded = encoder.fit_transform(X)
print(X_encoded) # [2 1 0 1 2]
```

只能处理一维数据！

### 独热

```py
import pandas as pd

df = pd.DataFrame({
    'Color': ['red', 'blue', 'green', 'red', 'blue'],
    'Size': ['S', 'M', 'L', 'M', 'S'],
    'Price': [100, 150, 200, 120, 180]
})
```

用 Pandas 实现独热编码：

```py
df_encoded = pd.get_dummies(df, columns=['Color', 'Size'])
print(df_encoded)

"""
   Price  Color_blue  Color_green  Color_red  Size_L  Size_M  Size_S
0    100       False        False       True   False   False    True
1    150        True        False      False   False    True   False
2    200       False         True      False    True   False   False
3    120       False        False       True   False    True   False
4    180        True        False      False   False   False    True
"""
```

用 Sklearn 实现独热编码，比较复杂（由 Deepseek 实现）：

```py
from sklearn.preprocessing import OneHotEncoder

encoder = OneHotEncoder(sparse_output=False)
categorical_cols = ['Color', 'Size']
encoded_array = encoder.fit_transform(df[categorical_cols])
df_encoded = pd.concat([
    df[['Price']].reset_index(drop=True),
    pd.DataFrame(encoded_array, columns=encoder.get_feature_names_out(categorical_cols))
], axis=1)
print(df_encoded)

"""
   Price  Color_blue  Color_green  Color_red  Size_L  Size_M  Size_S
0    100         0.0          0.0        1.0     0.0     0.0     1.0
1    150         1.0          0.0        0.0     0.0     1.0     0.0
2    200         0.0          1.0        0.0     1.0     0.0     0.0
3    120         0.0          0.0        1.0     0.0     1.0     0.0
4    180         1.0          0.0        0.0     0.0     0.0     1.0
"""
```

- `sparse_output=False` 是因为默认的输出是 `scipy` 的稀疏矩阵，为了正常的输出。
- `OneHotEncoder` 对所有列都做独热编码，所以需要把输出 `cat` 起来。

## Pipeline

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

# Training

- `sklearn.linear_model`
  - `LinearRegression` / `Lasso` / `Ridge`
  - `LogisticRegression`
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

print(y_pred)
```

# Metrics

## MSE & $R^2$

```py
from sklearn.metrics import mean_squared_error, r2_score

mse = mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)
```

## 混淆矩阵

```py
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score

accuracy = accuracy_score(y_test, y_pred)
precision = precision_score(y_test, y_pred)
recall = recall_score(y_test, y_pred)
f1 = f1_score(y_test, y_pred)
```