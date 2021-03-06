# AlternateColors2
作者：王聿中

关键词：计数 枚举
## 题目简述
初始你有$$r$$个红球、$$g$$个绿球、$$b$$个蓝球。有一个机器人每回合都会按照红绿蓝的顺序摧毁每种颜色的球各一个（如果某种颜色的球当前已无剩余则忽略该颜色）。若干回合后，所有的$$n=r+g+b$$个球均被摧毁，并且第$$k$$个被摧毁的球是红球。已知$$n, k$$，求有多少种可能的初始状态。

$$1\leq k\leq n\leq 100000$$

## 算法一
对于此题，我们很容易想到枚举。我们尝试枚举$$r, g$$，那么$$b=n-r-g$$。然后，对于每组$$\left( r,g,b\right)$$，我们判断它们作为初始情况是否合法并，统计合法的情况数。

对于初始情况$$\left( r,g,b\right)$$判断第$$k$$个被摧毁的求是否为红球，我们当然可以用$$O\left( n\right)$$时间进行模拟，并求出第$$k$$个被摧毁的球的颜色。然而，显然地，我们可以加速这个模拟的过程。

我们注意到，机器人摧毁所有球的整个过程可以被分为三个部分，每个部分都包含若干（可能为$$0$$）个连续的回合。第一部分中，机器人每回合摧毁3个球；第二部分中，机器人每回合摧毁2个球；第三部分中，机器人每回合摧毁1个球。每个部分中，机器人所有的行动均相同。并且我们发现，第一部分的回合数即为$$r, g, b$$中的最小值，前两部分的回合数即为$$r, g, b$$中的次大值，总回合数即为$$r, g, b$$中的最大值。

那么，我们就可以判断第$$k$$个被摧毁的球是在哪一个部分被摧毁的，再通过取模运算，我们就很容易求得该球的颜色了。

由于之前枚举的时间复杂度为$$O\left( {n}^{2}\right)$$，因此这个算法的时间复杂度是$$O\left( {n}^{2}\right)$$的。

## 分析
算法一时间复杂度显然不足以通过此题，我们尝试寻找更优秀的算法。

我们先考虑一个简化版的问题：假设蓝球的个数为零，即球的颜色只有红色、绿色2种。

在这个简化版的问题中，我们前面提到的“第一部分”就不存在了。那么就只存在两种可能性：第$$k$$个球在第二部分或第三部分被摧毁。我们发现，当且仅当$$k$$为奇数时，其才有可能在第二部分被摧毁，这时第二部分的长度（即$$min\left( r,g\right)$$）至少为$$\frac{k+1}{2}$$，则剩余的$$n-k-1$$个球的染色共有$$n-k$$种方案（球无区别）。而如果其在第三部分被摧毁，那么$$g<\lfloor \frac{k+1}{2}\rfloor$$，所以$$r, g$$的取值共有$$\lfloor \frac{k+1}{2}\rfloor$$种方案。

可以发现，我们解决这个简化版问题的算法的时间复杂度是$$O\left( 1\right)$$的。

## 算法二
基于分析，我们希望把原问题转化为这个简化版问题。

首先，如果第$$k$$个被摧毁的球是在第一部分被摧毁的，那么需满足$$k\space mod\space 3=1$$且$$min\left( r,g,b\right)\geq\frac{k+2}{3}$$，则剩余的$$n-k-2$$个球的染色共有$$\left( n-k\right)\times\left( n-k+1\right)$$种方案。

如果第$$k$$个被摧毁的球不是在第一部分被摧毁的，那么我们只需枚举第一部分的长度$$i$$，即可转化为简化版问题。为了方便起见，我们不妨假设$$g\geq b$$，计算对答案的贡献时乘2并减去$$g=b$$的情况即可。

至此，原问题已得到完美解决，时间复杂度为$$O\left( n\right)$$。

*注：我的代码中有部分细节与题解略有出入，但思路大体上一致*