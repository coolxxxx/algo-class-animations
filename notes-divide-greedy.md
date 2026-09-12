# C++ 分治与贪心 · 课堂包

配套：`interactive.html`（投影演示）+ 白板讲解片。

---

## 1. 概念对照（板书用）

| | 分治 | 贪心 |
|---|---|---|
| 一句话 | 大问题拆成子问题，解完再合并 | 每步都选当前看起来最优 |
| 三要素 | 分解 · 解决（递归） · 合并 | 贪心策略 · 选择 · 证明（交换论证/反证） |
| 经典 | 归并排序、快速排序、二分 | 活动选择、找零（特定币制）、哈夫曼 |
| 风险 | 合并写错、复杂度算错 | **以为贪心其实不对**（无证明就用） |
| 课上口诀 | 先拆到不能再拆，再合起来 | 想清楚：为什么局部最优=全局最优？ |

---

## 2. C++ 可编译骨架

### 归并排序

```cpp
#include <bits/stdc++.h>
using namespace std;

void merge(vector<int>& a, vector<int>& tmp, int lo, int mid, int hi) {
    int i = lo, j = mid, k = lo;
    while (i < mid && j < hi) {
        if (a[i] <= a[j]) tmp[k++] = a[i++];
        else              tmp[k++] = a[j++];
    }
    while (i < mid) tmp[k++] = a[i++];
    while (j < hi)  tmp[k++] = a[j++];
    for (int t = lo; t < hi; ++t) a[t] = tmp[t];
}

void mergeSort(vector<int>& a, vector<int>& tmp, int lo, int hi) {
    if (hi - lo <= 1) return;                 // 终止
    int mid = lo + (hi - lo) / 2;             // 分
    mergeSort(a, tmp, lo, mid);
    mergeSort(a, tmp, mid, hi);
    merge(a, tmp, lo, mid, hi);               // 合
}

int main() {
    vector<int> a = {38, 27, 43, 3, 9, 82, 10};
    vector<int> tmp(a.size());
    mergeSort(a, tmp, 0, (int)a.size());
    for (int x : a) cout << x << ' ';
    // 3 9 10 27 38 43 82
}
```

### 活动选择（贪心）

```cpp
#include <bits/stdc++.h>
using namespace std;

struct Act { int id, s, e; };

int selectActs(vector<Act> v) {
    sort(v.begin(), v.end(), [](const Act& a, const Act& b) {
        return a.e < b.e;                     // 结束早优先
    });
    int cnt = 0, lastEnd = 0;
    for (auto& a : v) {
        if (a.s >= lastEnd) { ++cnt; lastEnd = a.e; }
    }
    return cnt;
}
```

---

## 3. 课堂流程建议（45–60 分钟）

1. **5′ 钩子**：乱序扑克如何最快排好？开会如何安排最多场次？
2. **15′ 分治**：投影 `interactive.html` → 归并排序，学生喊「下一步」
3. **10′ 落地代码**：黑板默写 `merge` 双指针；强调 `<=` 稳定性
4. **15′ 贪心**：活动选择可视化；故意问「按开始时间行不行？」举反例
5. **10′ 做题**：下面第 1、3 题当堂；其余留作业
6. **5′ 总结**：分治会写 merge；贪心先想反例

---

## 4. 递进题单

### 分治

1. **基础**：对 `n≤1e5` 的数组排序，手写归并，输出前 10 个数。  
2. **逆序对**：归并过程中统计 `a[i] > a[j]` 的对数（提示：左段剩余元素都与 `a[j]` 构成逆序对）。  
3. **二分答案**：分治思想的非递归形态——在答案上二分。练习：求 `sqrt(x)` 整数部分，或「分割数组最大值最小」。

### 贪心

4. **基础**：活动选择，输出最多场次与方案编号。  
5. **找零**：币种为 `1,5,10,25`，证明贪心正确；若加入 `30` 则举反例。  
6. **区间覆盖**：用最少的点覆盖所有区间（按右端点排序，点放在右端点）。

### 对比思考题（课后）

7. 为什么「最大子段和」用 DP/Kadane 更自然，而不是简单贪心？  
8. 分治能解决的问题，是否都能写成迭代？举例说明栈的作用。

---

## 5. 验收清单（下课前自查）

- [ ] 学生能说出分治三段、贪心策略+为何对
- [ ] 学生能默写 merge 双指针
- [ ] 学生能指出一个「假贪心」反例
- [ ] 当堂至少完成 2 题
