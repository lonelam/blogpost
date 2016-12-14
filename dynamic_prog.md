---
title: 动态规划优化——学习笔记
---

[hrbust的ACMbook](https://hrbust-acm-team.gitbooks.io/acm-book/content/dynamic_programming/opt.html)
---

>[一道例题](https://uva.onlinejudge.org/external/4/473.pdf)
>题目太难读了，“The songs will be recorded on the set of disks in the order of the dates they were written.”这句话简直没法理解
但是仔细想想的话，也就是和最长上升子序列差不多的意思，不能够往回走的意思。~~

###题意：把$n$个数字，分成$m$组。每组的和不能大于$t$。分组必须是有序的，并且保证所有的数字都是小于$t$的。求最多能把多少数字划入分组里。
定义: $dp[i][j][k]$ 表示前面i个数字，分成了j组，最后一组还剩下的容量为k

$$
dp[i][j][k] = \begin{cases} max\{dp[i - 1][j][k - w[i]], dp[i  - 1][j][k]\} & k\geq w[i] \\ max(dp[i - 1][j][k], dp[i - 1][j - 1], dp[i - 1][j - 1][t - w[i]]) & k < w[i] \end{cases}
$$
这样的话， 于是空间复杂度$O(nmt)$ 时间复杂度也是$O(nmt)$
- 一种改进方式
$dp[i][j] = (x, y)$ 表示在前 $i$ 个数字里面要选到 $j$ 个以后用了 $(x, y), x 个组，最后一组还有y容量$

这样的话复杂度就只有 $O(n^2)$
那么状态怎么转移呢？和刚才的转移相似，如果选了 $i$ 那么
