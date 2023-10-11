# gcd与lcm

**b**可以被**a**整除 记作  $a \mid b$
**b**是**a**的倍数,**a**是**b**的约数(因数)
**C++14**自带``__gcd(a,b)``
**C++17**有``<numeric>``头 自带``std::gcd``和``std::lcm``

### 最大公约数
最大公约数即为 Greatest Common Divisor，常缩写为 gcd。
一组整数的公约数，是指同时是这组数中每一个数的约数的数。$\pm 1$ 是任意一组整数的公约数。
一组整数的最大公约数，是指所有公约数里面最大的一个。
有``gcd(a,b)==gcd(b,a%b)``

##### 多个数的**gcd**
就是每相邻两个数的约数

时间复杂度$O(log \max(a,b))$
```cpp
int gcd(int a, int b)
{
    return b == 0 ? a : gcd(b, a % b);
}
int gcd(int a, int b)
{
    while (b != 0)
    {
        int tmp = a;
        a = b;
        b = tmp % b;
    }
    return a;
}
```

互素``gcd(a,b)==1``
```c++
bool Isgcd(int a, int b)
{
	if (a == 1 || b == 1)     // 两个正整数中，只有其中一个数值为1，两个正整数为互质数
		return true;
	while (1)
	{          // 求出两个正整数的最大公约数
		int t = a % b;
		if (t == 0)
		{
			break;
		}
		else
		{
			a = b;
			b = t;
		}
	}
	if (b > 1)	return false;// 如果最大公约数大于1，表示两个正整数不互质
	else return true;	// 如果最大公约数等于1,表示两个正整数互质
}
```
### 最大公倍数

一组整数的公倍数，是指同时是这组数中每一个数的倍数的数。0 是任意一组整数的公倍数。
一组整数的最小公倍数，是指所有正的公倍数里面，最小的一个数。
结论``gcd(a,b)*lcm(a,b)==a*b``

##### 多个数的**lcm**
当我们算出两个数的 $\gcd$，或许在求多个数的 $\gcd$ 时候，我们将它放入序列对后面的数继续求解，那么，我们转换一下，直接将最小公倍数放入序列即可。

```cpp
int lcm(int a, int b)
{
	//不a*b 防止爆longlong
	return a / gcd(a, b) * b;	
}
```