# 七～八级题单与骨架

配套讲义：`gesp-L7-8.md` · 真题官网：https://gesp.ccf.org.cn/101/1010/index.html  
前置展示台：BFS/DFS/树/DP/位运算/排序（见首页知识点分区）

---

## A. BFS 最短路（dist）

```cpp
// 无权图：最少边数
queue<int> q;
dist[s]=0; q.push(s);
while(!q.empty()){
    int u=q.front(); q.pop();
    for(int v:g[u]) if(dist[v]<0){
        dist[v]=dist[u]+1; q.push(v);
    }
}
```

题：网格 4 邻接最短；解释 dist 含义；何时不能用 BFS（负权）。

---

## B. 树遍历互推

```text
先序: A B D E C F G
中序: D B E A F C G
→ 根A，中序左 D B E / 右 F C G
→ 后序: D E B F G C A
```

题：10 组先序+中序练后序；只给中序+后序求先序。

---

## C. Kruskal 选边

```cpp
sort(edges by w);
DSU 初始化;
for e in edges:
    if find(u)!=find(v): unite; 选中 e;
```

题：按讲义边集手勾第 1/2/3 条；Prim 与 Kruskal 何时等价。

---

## D. 区间 DP / 石子合并（入门）

```cpp
// 合并代价 = 左堆和+右堆和；求最小总代价
// dp[l][r] = min(dp[l][k]+dp[k+1][r]+sum(l,r))
```

题：三堆 1 2 3；四堆手推；对比贪心「每次选最小两堆」反例。

---

## E. LCS / 背包（DP 表）

LCS：相等 `dp[i][j]=dp[i-1][j-1]+1`，否则 `max(左,上)`。  
01 背包一维：**逆序** `for v=W; v>=w; v--`。

题：`abc/ac`；`abcb/bdcab`；背包 W=8 跟算 dp[8]。

---

## F. 快速幂

```cpp
long long powmod(long long a, long long n, long long mod){
    long long r=1%mod; a%=mod;
    while(n){ if(n&1) r=r*a%mod; a=a*a%mod; n>>=1; }
    return r;
}
```

题：`2^10` 步数；`n` 很大时为何 O(log n)。

---

## G. 哈希表语义

冲突必有；链地址拉链；开放定址往后探。  
题：选择题「哪句正确」；手算简单开放定址插入。

---

## H. 差分 / 前缀和

区间加 `[l,r]+x`：`d[l]+=x; d[r+1]-=x`；最后前缀和还原。  
题：复杂度 O(n+m)；与暴力 O(nm) 对比。

---

## 模考建议

1. 限时做官网最近一期 **C++ 七级** 选择 15 题  
2. 错题按本表 A–H 归类  
3. 再做 **八级** 组合/图论部分  
4. 展示台补前置课（若 BFS/树不熟）
