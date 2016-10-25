# CheckerFreeness
作者：汪乐平

关键词：凸四边形判定 压位

## 题目简述

给出$$W$$个白点和$$B$$个黑点，保证没有重点，且任意三点不共线。问是否存在一个凸四边形，满足一对相对的顶点均为白点，另一对相对的顶点均为黑点。$$1\leq W,B\leq 222,1\leq x,y\leq 10000000$$。

## 算法一

枚举每一对白点和黑点，显然四边形是凸的当且仅当对角线是相交的，所以用叉积判断两个白点连成的线段和两个黑点连成的线段是否相交即可，时间复杂度$$O(W^2B^2)$$。

## 算法二

换一种方法判断是否是凸四边形。选出一个黑点和两个白点，那么另一个黑点在下图所示的深色区域时这个四边形才是凸的：
[pic=https://apps.topcoder.com/wiki/download/attachments/93652627/d15002.png]