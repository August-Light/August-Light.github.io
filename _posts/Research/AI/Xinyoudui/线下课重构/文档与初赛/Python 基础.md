# 算法

- `sort` 和 `sorted` 都是 stable sort。
  - `reverse=True` 的作用不是先排序完再 `reverse`，而是反转每一次比较的结果。因此即使开了 `reverse` 依然是 stable 的。

# collections.Counter

`collections.Counter` 是一个内置的计数器。

```py
from collections import Counter
```

我们可以用可迭代的 object 创建一个 `Counter`：

```py
c1 = Counter({'a': 3, 'b': 2, 'c': 1})
c2 = Counter(['a', 'b', 'a', 'c', 'b', 'a'])
c3 = Counter("abacba")
```

使用方法：

```py
c = Counter({'a': 3, 'b': 2, 'c': 1})

# 获取元素出现次数
print(c['a'])  # 3
print(c['d'])  # 不存在的键返回 0，不抛 KeyError

# 获取所有元素
print(list(c.elements())) # ['a', 'a', 'a', 'b', 'b', 'c']

# 以二元组形式获取所有元素
print(c.items()) # dict_items([('a', 3), ('b', 2), ('c', 1)])

# 以二元组形式获取最常见元素
print(c.most_common(2)) # [('a', 3), ('b', 2)]
```

## 例题（卷 1 编程题 1）

请使用 Python 实现以下功能：

- 函数名为 `count_and_sort`，接收一个字符串列表 `data` 作为参数；
- 统计列表中每个字符串的出现次数；
- 按 “出现次数降序” 排序，次数相同的按字符串在原列表中 “首次出现顺序” 排序；
- 返回排序后的结果列表（每个元素为元组 `(字符串, 次数)`）。

【示例】：

输入：`["apple", "banana", "apple", "orange", "banana", "banana"]`

输出：`[("banana", 3), ("apple", 2), ("orange", 1)]`

```py
from collections import Counter

def count_and_sort(data):
    counter = Counter(data)
    result = sorted(counter.items(), key=lambda x: x[1], reverse=True)
    return result
```