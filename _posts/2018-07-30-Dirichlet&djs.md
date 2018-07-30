---
layout: post
title: 反演&积性函数前缀和&狄利克雷卷积
category: 题解
---

## 反演&积性函数前缀和&狄利克雷卷积

---
**时刻记住狄利克雷卷积定义：**$c(n)=\sum_ {i\|n} a(i)b(\frac{n}{i})$  

(这里的 = 没有赋值的意思）  
在本文中的一些基本定义：  
$e(x)=[x=1]$  （只有x=1时值才为一，其他时候值为0）

$id_ k(x)=x^k$  

$\phi(x)=\sum_ {i=1}^{x} [gcd(i,x)=1]$

$a \otimes b$表示$a$和$b$的狄利克雷卷积  
>
任何函数$\otimes e$还是它本身，所以$e$是单位元。  
看到$\sum_ {i\|n}f(i) $ 时可以想一想是不是$f \otimes id_ 0$(记住卷积定义）  

### 几个证明  

---
$\sum_ {d\|n}\mu(d)=[n=1]$  
($\mu \otimes id_ 0=e$)

现在<del>江</del>将$n$进行质因数分解，得到：  
$n=p_ 1^{m_ 1}p_ 2^{m_ 2}..p_ k^{m_ 1}$  
令$n^*=p_ 1p_ 2..p_ k$  

根据$\mu$的定义，假如说$d$有平方项，那$\mu(d)$为零。  
所以$\sum_ {d\|n} \mu(d)=\sum_ {d\|n^*} \mu(d)=\sum_ {i=0}^k (^k_ i)(-1)^i$  
观察二项式展开的样子：  
$(1+x)^k=\sum_ {i=0}^k(^k_ i)x^i$  
把$x=-1$带进来  
所以$\sum_ {d\|n} \mu(d)=(1-1)^k$

---
$\sum_ {i\|x}\phi(i)=id_ 1(x)$  
($\phi \otimes id_ 0 = id_ 1$)  
这里就是把1~n-1/n的所有数列出来。  
$\frac{1}{n},\frac{2}{n},\frac{3}{n},\frac{4}{n},\frac{5}{n},...$  
($n=6$时原数列为$\frac{1}{6},\frac{1}{3},\frac{1}{2},\frac{2}{3},\frac{5}{6}$)  

假如说$n$与某个数$i$有$gcd(i,n)>1$，那么他可以和$n$同时除掉这个$gcd$  
然后这样就得到了一个新的数列，其中分子与分母互质。  
对于任何一个小于$n$的$i$,$\frac{i}{n}$一定可以被化简成分母为$n$的因数的一个最简分数  
对于任何一个$i\|n$的$i$，与$gcd(i,j)==1\&j<i$的$j$构成的分数$\frac{j}{i}$也一定能找到与之相等的$\frac{k}{n}$  
所以就相等了

### 一个 Interesting 的性质  

---
现在有函数$F(x)=\sum_ {i\|x} f(i)$，而且知道$F(x)$要求$f(x)$  
把原式子写成卷积的形式：$F=f \otimes id_ 0$  
同时卷一下$\mu$  
$F \otimes \mu = f \otimes id_ 0 \otimes \mu$  
然而前面证明了$\mu \otimes id_ 0=e$  
所以$F \otimes \mu=f \otimes e =f$  
反..反演


### 计算一类积性函数的前缀和

---
这里定义$F$是$f$的前缀和。  
现在，对于一个函数$f$，找两个易求前缀和的函数$f^*$和$f^+$，使得：  

$f^* \otimes f =f^+$

则$F^+(n)=\sum_ {i=1}^n \sum _{d\|i}$$f(d)f^*(\frac{i}{d})$  

把对每个数枚举因数改为枚举因数找倍数  
$F^+(n)=\sum_ {1=1}^nf^ *(i) \sum_ {j=1}^{\lfloor \frac{n}{i} \rfloor}f(j)=\sum_ {i=1} ^nf^ *(i)F(\lfloor \frac{n}{i} \rfloor)$  
把$i=1$的情况单独提取出来  
$F^ +(n)=f^ *(1)F(n)+\sum_ {i=2} ^nf^ *(i)F(\lfloor \frac{n}{i} \rfloor)$  
对于积性函数有一个很显然的性质：$a(1)$=1或0，否则不满足$f(a) * f(b)=f(ab)$  
为0时没有任何意义，所以我们构造的时候不会选择一个$f(x)=0$的函数,所以  
$F^ +(n) = F(n)+\sum_ {i=2} ^nf^ *(i)F(\lfloor \frac{n}{i} \rfloor)$  
$F(n)=F^ +(n)-\sum_ {i=2} ^nf^ *(i)F(\lfloor \frac{n}{i} \rfloor)$  
这样先递推$F(n)$到$n^{\frac{2}{3}}$级别的位置  
然后记忆化一下 $F( \lfloor \frac{n}{i} \rfloor )$  