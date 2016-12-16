---
title: 动态规划优化——学习笔记
---

原题和分析[hrbust的ACMbook](https://hrbust-acm-team.gitbooks.io/acm-book/content/dynamic_programming/opt.html)
---

>[一道例题](https://uva.onlinejudge.org/external/4/473.pdf)
>题目太难读了，“The songs will be recorded on the set of disks in the order of the dates they were written.”这句话简直没法理解
但是仔细想想的话，大概就是说把songs选一些出来然后切段~~

### 题意：把 $n$ 个数字，分成$m$组。每组的和不能大于$t$。分组必须是有序的，并且保证所有的数字都是小于$t$的。求最多能把多少数字划入分组里。
定义: $dp[i][j][k]$ 表示前面i个数字，分成了j组，最后一组还剩下的容量为k

$$
dp[i][j][k] = \begin{cases}
max\{dp[i - 1][j][k - w[i]], dp[i - 1][j][k]\} & k\geq w[i] \\\\
max(dp[i - 1][j][k], dp[i - 1][j - 1], dp[i - 1][j - 1][t - w[i]]) & k < w[i]
\end{cases}
$$

这样的话， 于是空间复杂度$O(nmt)$ 时间复杂度也是$O(nmt)$
- 一种改进方式
$dp[i][j] = (x, y)$ 表示在前 $i$ 个数字里面要选到 $j$ 个以后用了 $(x, y), x 个组，最后一组还有y容量$

这样的话复杂度就只有 $O(n^2)$
那么状态怎么转移呢？和刚才的转移相似，如果选了 $i$ 那么要么开新的一组要么就放进$y$里面。
递推式是
$$
dp[i][j] = \begin{cases}
min (dp[i - 1][j], dp[i - 1][j - 1]y - w[i]) & if & dp[i - 1][j].y \geq w[i] \\\\ min(dp[i - 1][j], \{dp[i - 1][j - 1]x+1 , (t)\} & if & dp[i - 1][j].y < w[i] \end{cases}
$$

其中$min$表示
$$
x_i < x_j or (x_i = x_j and y_i > y_j)
$$

## 决策单调性·四边形不等式
>
>在一个操场上摆放着一排$n$堆石子。现要将石子有次序地合并成一堆。规定每次只能选相邻的2堆石子合并成新的一堆，并将新的一堆石子数记为该次合并的得分。求出将  堆石子合并成一堆的最小得分和最大得分以及相应的合并方案。
