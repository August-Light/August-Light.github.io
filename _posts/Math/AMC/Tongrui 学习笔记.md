# Chapter 1.1 导角

## Page 5 

TODO:

## Page 6 [2002 AIME II #14](https://artofproblemsolving.com/wiki/index.php?title=2002_AIME_II_Problems/Problem_14)

> 直角三角形 $APM$ 中，$A$ 是直角，周长为 $152$。在边 $AP$ 上取一点 $O$ 为圆心画一个半径为 $19$ 的圆，正好和 $AM$ 与 $PM$ 都相切。求 $OP$。

拿到题目的第一反应是用勾股定理列一堆方程开始硬解。但是显然非常麻烦！

但是根据 [2019 AIME I #11](https://artofproblemsolving.com/wiki/index.php?title=2019_AIME_I_Problems/Problem_11) 的经验，我们可以用**三角函数**来刻画这个问题。

$$19 (1 + 2 \cot \theta + \tan 2 \theta + \sec 2 \theta) = 152$$

$$2 \cot \theta + \tan 2 \theta + \sec 2 \theta = 7$$

（最终要求的东西是 $19 \sec 2 \theta$）

同时出现一个 $\theta$ 和两个 $2 \theta$，半倍角公式或许能做，但是**万能公式**是一个不错的选择。

设 $t = \tan \theta$，有 $\tan 2 \theta = \frac {2t} {1 - t^2}$，$\sec 2 \theta = \frac {1 + t^2} {1 - t^2}$。

$$\frac 2 t + \frac {2t} {1 - t^2} + \frac {1 + t^2} {1 - t^2} = 7$$

解出 $t = \frac 1 2$，$\sec 2 \theta = \frac 5 3$。

答案为 $19 \times \frac 5 3 = \boxed{\frac {95} 3}$。

## Page 8



# Chapter 1.2.1 鸡爪定理



# Chapter 1.2.2


# Chapter 1.2.3 Miquel 点

# Chapter 1.2.4 Simson 线