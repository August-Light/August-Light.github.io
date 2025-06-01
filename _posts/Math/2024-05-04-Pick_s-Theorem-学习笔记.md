---
title: "Pick's Theorem 学习笔记"
date: 2024-05-04
permalink: /posts/2024/05/Pick_s-Theorem-学习笔记/
excerpt: '格点多边形的内部整点数量计算。'
tags:
  - OI
  - 专题笔记
---

# Pick's Theorem 学习笔记

[UVA10088 题目传送门](https://www.luogu.com.cn/problem/UVA10088)

题意：顺时针或逆时针地给出一个 $n$ 个顶点（**顶点都是整点**）的简单多边形，求这个多边形**内部**的**整点**数量（位于多边形形上的整点不算）。

## Pick's Theorem

对于一个顶点都是整点的简单多边形：

令 $I$ 为多边形内部的整点数量，$B$ 为多边形形上的整点数量，$A$ 为多边形面积。有公式：

$$A = I + \dfrac B 2 - 1$$

比较有用的是它的变形：

$$I = A - \dfrac B 2 + 1$$

## Pick's Theorem 的证明

对于一个 $B = 3$ 的三角形，其面积 $A$ 必然为 $\dfrac 1 2$。

采用数学归纳法的思路：将多边形剖成若干个 $B=3$ 的三角形，每次切除一个三角形，要么减少一个边上的点，要么将一个内部的点转化为边上的点，直到把多边形切成一个只有两点的线段。

因此 $A = \dfrac 1 2 (2I + B - 2) = I + \dfrac B 2 - 1$。

![Pick's Theorem from Wikipedia](https://cdn.luogu.com.cn/upload/image_hosting/hhrg8pwi.png)

## 关于 Pick's Theorem

皮克定理有许多有趣的应用，可以看 [Matrix67 的这篇文章](http://www.matrix67.com/blog/archives/2199)。

相关练习：[P2735 [USACO3.4] 网 Electric Fences](https://www.luogu.com.cn/problem/P2735)

## 此题解法

利用向量叉积求出多边形面积 $A$，用一点简单数论求出 $B$，再用 Pick's Theorem 即可求出 $I$。

```cpp
#include <bits/stdc++.h>
#define gcd __gcd
using namespace std;
typedef long long ll;

const int MAXN = 1000 + 5;

struct Point {
    ll x, y;
    Point(ll x, ll y) : x(x), y(y) {}
};
ll cross(Point &a, Point &b) {
    return a.x * b.y - a.y * b.x;
}

int n;
vector<Point> points;

int main() { ios::sync_with_stdio(0); cin.tie(0);
    while (1) {
        cin >> n;
        if (n == 0)
            break;
        for (int i = 1; i <= n; i++) {
            int x, y; cin >> x >> y;
            points.emplace_back(x, y);
        }
        points.push_back(points[0]);

        ll area = 0, edge = 0;
        for (int i = 1; i <= n; i++) {
            auto &a = points[i-1], &b = points[i];
            ll dx = abs(b.x - a.x), dy = abs(b.y - a.y);
            area += cross(a, b);
            edge += gcd(dx, dy);
        }

        area = abs(area) / 2;

        cout << area - edge / 2 + 1 << '\n';

        points.clear();
    }
    return 0;
}
```

## 参考

- [Pick's Theorem - Art of Problem Solving](https://artofproblemsolving.com/wiki/index.php/Pick%27s_Theorem)
- 图片来自 [Pick's theorem - Wikipedia](https://en.wikipedia.org/wiki/Pick%27s_theorem)