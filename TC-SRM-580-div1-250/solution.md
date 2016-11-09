# EelAndRabbit

作者：杨家齐

关键词：离散化, 暴力

## 题目简述

河里有 $$n$$ 条鱼, 每条鱼的速度都为 $$1$$, 第 $$i$$ 条鱼的长度为 $$l_i$$, 并且会在 $$t_i$$ 时刻出现在 $$0$$ 坐标处. 也就是说, 对于任意的时刻 $$T$$, 第 $$i$$ 条鱼的头在坐标 $$T - t_i$$ 处, 尾巴在 $$T - t_i - l_i$$ 处.

你一直站在坐标 $$0$$ 处, 并且计划抓(至多)两次鱼, 每次抓的时候你会同时把所有能抓到的鱼都抓上来. 你能抓到一条鱼**当且仅当**那条鱼在你的面前(包括头和尾).

求你最多能抓到多少条鱼.

## 限制与约定

$$1 \le n \le 50, 1 \le l_i \le 10^9, 0 \le t_i \le 10^9$$.

## 算法

实际上, 我们只需要考虑所有形如 $$t_i$$ 以及 $$t_i + l_i$$ 的时刻 $$T$$ 就可以了. 如果我们抓鱼的时间不能表示成这两种形式之一的话, 我们可以通过改变时间 $$T$$ 调整到这两种形式.

因此我们不妨枚举两次抓鱼的时刻 $$T_1$$ 和 $$T_2$$, 然后统计有多少条鱼能被抓上来, 并求出鱼的数量的最大值.

时间复杂度: $$O(n^3)$$.