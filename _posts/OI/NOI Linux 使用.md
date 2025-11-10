# 注意事项

- VSCode
  - 开始写代码前，先去改好 Auto save。

# 编译

```
g++ [NAME].cpp -o [NAME] -O2 -std=c++14 -Wall -Wextra -fsanitize=undefined
```

- `-Wall -Wextra` 增加 Warning。
- `-fsanitize=undefined` 开启 UB 检测器。
- 栈空间：
  - `ulimit -a` 查看空间情况。
  - `ulimit -s [k]` 将栈空间改为 $k$ KiB，即 $\frac k {1024}$ MiB。$k$ 也可以干脆直接调成 `unlimited`。

# 运行

```
./[NAME]
```

不要在命令行输入输出（软件有 bug），建议输入走文件流。

```
./[NAME] <[NAME].in >[NAME].out
```

这样不写 `freopen` 也能走文件输入输出。

# 对拍

## 随机数据生成

初始化：（$64$ 位随机数的话改为 `mt19937_64`）

```cpp
mt19937 Rand(time(0));
```

在 $[l,r]$ 中均匀随机一个数：

```cpp
int rn(int l, int r) {
    uniform_int_distribution<int> distr(l, r);
    return distr(Rand);
}
```

打乱一个序列：

```cpp
    shuffle(a+1, a+n+1, Rand); // Rand 为一个随机数生成器
```

## checker

用 `diff` 命令比较文件，其中 `-Bb` 表示忽略空白字符和换行：

```cpp
    system("g++ [NAME].cpp -o [NAME] -O2 -std=c++14 -Wall -Wextra");
    system("g++ BRUTEFORCE.cpp -o BRUTEFORCE -O2 -std=c++14 -Wall -Wextra");
    system("g++ GEN.cpp -o GEN -O2 -std=c++14 -Wall -Wextra");
    while (true) {
        system("./GEN >[NAME].in");
        system("./BRUTEFORCE <[NAME].in >[NAME].ans");
        system("./[NAME] <[NAME].in >[NAME].out");
        if (system("diff [NAME].out [NAME].ans -Bb"))
            break;
    }
```

# Reference

- [NOI 系列赛常见技术问题整理](https://www.luogu.com.cn/article/kgofa37e)