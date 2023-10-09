# Tarjan

Tarjan算法的用途

1. 求桥和割点
2. 求点和边的双连通分量
3. .求强连通





此算法最重要的是维护两个数组

1，DFN［］作为这个点搜索的次序编号（时间戳），简单来说就是 第几个被搜索到的。％每个点的时间戳都不一样％。

2，LOW［］作为每个点在这颗树中的，最小的子树的根，每次保证最小，like它的父亲结点的时间戳这种感觉。如果它自己的LOW［］最小，那这个点就应该从新分配，变成这个强连通分量子树的根节点。

PS：每次找到一个新点，这个点LOW［］＝DFN［］。

```c++






void tarjan(int now)
{
    dfn[now]=low[now]=++cnt;//初始化dfn数组，同时将low设置为相同值
    stk[++t]=now;//入栈操作
    vis[now]=true;//v[]代表该点是否已入栈
    for(int i=head[now];i;i=edge[i].next)
    {
        int to=edge[i].to;
        if(dfn[to]==0)
        {
            tarjan(to);
            low[now]=min(low[now],low[to]);//回溯时更新low[ ]，取最小值
        }
        else if(vis[to]==true)
            low[now]=min(low[now],dfn[to]);
            //一旦遇到已入栈的点，就将该点作为连通量的根
            //这里用dfn[to]更新的原因是：这个点可能
            //已经在另一个强连通分量中了但暂时尚未出栈，所
            //以now不一定能到达low[to]但一定能到达
            //dfn[to].
    }
    if(dfn[now]==low[now])
    {
        int cur;
        do{
            cur=stk[t--];//出栈
            vis[cur]=false;
        }while(now!=cur);
    }
}
```

