# 查找与搜索题单（二分 / BFS / DFS）

配套：`?lesson=cpp5-3` `cpp6-7` `cpp6-8` · VOX `vox-binary` / `vox-bfs` / `vox-dfs`

GESP 真题：https://gesp.ccf.org.cn/101/1010/index.html  
建议对照：五级/六级「二分答案、迷宫、全排列」编程题。

---

## 1. 二分查找

**前提**：有序。**动作**：lo/hi 夹逼，mid 试值。

```cpp
int lo = 0, hi = n - 1, ans = -1;
while (lo <= hi) {
    int mid = lo + (hi - lo) / 2;
    if (a[mid] == target) { ans = mid; break; }
    if (a[mid] < target) lo = mid + 1;
    else hi = mid - 1;
}
```

题：  
1. 手推找 `7` 时 lo/hi/mid 序列。  
2. 找不存在的数，ans 是多少。  
3. 改成「第一个 ≥ x 的位置」（lower_bound）。  
4. 100 个数最多几次？（7）

---

## 2. BFS 最短路

队列；先到必最短。

```cpp
// 迷宫 0 可走，从 (0,0) 到 (n-1,m-1)
queue<pair<int,int>> q;
q.push({0,0}); dist[0][0] = 0; vis[0][0] = 1;
int dx[] = {1,-1,0,0}, dy[] = {0,0,1,-1};
while (!q.empty()) {
    auto [x,y] = q.front(); q.pop();
    for (int k = 0; k < 4; k++) {
        int nx = x+dx[k], ny = y+dy[k];
        if (nx<0||ny<0||nx>=n||ny>=m) continue;
        if (g[nx][ny] || vis[nx][ny]) continue;
        vis[nx][ny] = 1;
        dist[nx][ny] = dist[x][y] + 1;
        q.push({nx,ny});
    }
}
```

题：  
1. 给 6×6 迷宫手标距离层。  
2. 堵一条路，最短步数变吗？  
3. 为什么不用栈做最短路？

---

## 3. DFS 全排列 / 回溯

used 标记；选满输出后擦标记。

```cpp
void dfs(int k) {
    if (k > n) { 输出 path; return; }
    for (int i = 1; i <= n; i++) if (!used[i]) {
        used[i] = 1; path[k] = i; dfs(k+1); used[i] = 0;
    }
}
```

题：  
1. n=3 手写 6 种排列。  
2. n=4 多少种？（24）  
3. 演示 used 从 1 变回 0 的「回溯瞬间」。

---

## 4. 易错

- 二分 `mid` 溢出 → `lo+(hi-lo)/2`  
- BFS 忘标记导致重复入队  
- DFS 忘清 `used` → 排列残缺

**GESP**：六级迷宫/排列类题，先画图再写码。
