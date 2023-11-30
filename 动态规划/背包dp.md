# 背包dp

有 $n$ 个物品和一个容量为 $W$ 的背包，每个物品有重量 $w_{i}$ 和价值 $v_{i}$ 两种属性，

要求选若干物品放入背包使背包中物品的总价值最大且背包中物品的总重量不超过背包的容量。
### 1. 0-1背包

每种物品一个 至多能选一次

时间$O(NC)$ 空间$O(NC)$ 

```cpp
int dp[1010][1010];
void slove()
{
	int n, W;
	std::cin >> W >> n;
	std::vector<int> w(n + 1), v(n + 1);
	for (int i = 1; i <= n; i++)
		std::cin >> w[i] >> v[i];
	for (int i = 1; i <= n; i++)
		for (int j = 0; j <= W; j++)
		{
			if (j < w[i])
				dp[i][j] = dp[i - 1][j];
			else
				dp[i][j] = std::max(dp[i - 1][j], dp[i - 1][j - w[i]] + v[i]);
		}
	std::cout << dp[n][W] << "\n";
}
```
滚动数组优化空间$O(C)$
```cpp
int dp[1010];
void slove()
{
	int n, W;
	std::cin >> W >> n;
	std::vector<int> w(n + 1), v(n + 1);
	for (int i = 1; i <= n; i++)
		std::cin >> w[i] >> v[i];
	for (int i = 1; i <= n; i++)
		for (int j = W; j >= w[i]; j--)
			dp[j] = std::max(dp[j], dp[j - w[i]] + v[i]);
	std::cout << dp[W] << "\n";
}
```

---

### 2. 完全背包

每种物品多个 能选多次
```cpp
int dp[N];
void slove()
{
	int n, W;
	std::cin >> W >> n;
	std::vector<int> w(n + 1), v(n + 1);
	for (int i = 1; i <= n; i++)
		std::cin >> w[i] >> v[i];
	for (int i = 1; i <= n; i++)
		for (int j = w[i]; j <= W; j++)
				dp[j] = std::max(dp[j], dp[j - w[i]] + v[i]);
	std::cout << dp[W] << "\n";
}
```

### 3. 多重背包
每种物品k个

```cpp
int dp[N];
void slove()
{
	int n, W;
	std::cin >> W >> n;
	std::vector<int> v, w;
	for (int i = 1, vt, wt, ct; i <= n; i++)
	{
		std::cin >> wt >> vt >> ct;
		for (int j = 1; j <= ct; j *= 2, ct -= j)
		{
			v.push_back(j * ct);
			w.push_back(j * wt);
		}
		if (ct > 0)                                  
		{
			v.push_back(ct * vt);
			w.push_back(ct * wt);
		}
	}
	int len = v.size();
	for (int i = 0; i < len; i++)
		for (int j = W; j >= w[i]; j--)
			dp[j] = std::max(dp[j], dp[j - w[i]] + v[i]);
	std::cout << dp[W] << "\n";
}
```
### 4. 混合背包

