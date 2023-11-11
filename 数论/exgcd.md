# exgcd


### 裴蜀定理

设 $a,b$为正整数，则关于$ax+by=c$的方程有整数解当且仅当是 $gcd(a,b)$的倍数。

扩展欧几里得算法

求不定方程$ax+by=c$的一组解


```cpp
// 返回gcd(a,b) 并返回ax+by=gcd(a,b)的x,y的特解
int exgcd(int a, int b, int &x, int &y)
{
    if (b == 0)
    {
        x = 1;
        y = 0;
        return a;
    }
    int d=exgcd(b, a % b, x, y);
    y -= a / b * x;
    return d;
}
```