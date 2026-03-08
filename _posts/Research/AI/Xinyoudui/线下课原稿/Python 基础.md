# 实用

- `help(func)` 会给出 `func` 的文档。
- `sort` 和 `sorted` 都是 stable sort。
  - `reverse=True` 的作用不是先排序完再 `reverse`，而是反转每一次比较的结果。因此即使开了 `reverse` 依然是 stable 的。
- 拼接 $n$ 个字符，使用 `+` 或 `+=` 的时间复杂度都是 $\Theta(n^2)$，因为Python 的字符串是不可变对象。
  - 使用 `join` 拼接字符串可以保证线性。
  - 💡 CPython 可能会优化，但是这不可靠。

# collections.Counter

```py
c1 = Counter(['a', 'b', 'a', 'c', 'b', 'a'])
c2 = Counter({'a': 3, 'b': 2, 'c': 1})
c3 = Counter("abacaba")
```

```py
c = Counter(['a', 'b', 'a', 'c'])

# 访问计数
print(c['a'])  # 2
print(c['d'])  # 0（不存在的键返回0，不会抛出KeyError）

# 获取所有元素
print(list(c.elements()))  # ['a', 'a', 'b', 'c']

# 获取最常见元素
print(c.most_common(2))  # [('a', 2), ('b', 1)]
print(c.most_common())   # [('a', 2), ('b', 1), ('c', 1)]
```

例：

```py
from collections import Counter

def count_and_sort(data):
    counter = Counter(data)
    result = sorted(counter.items(), key=lambda x: x[1], reverse=True)
    return result
```