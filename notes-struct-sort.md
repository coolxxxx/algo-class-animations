# C++ 结构体数组排序 · 课堂包（第二讲）

配套：`easy_sort.html` + 白板片。基于讲义 33/34。

---

## 1. 为什么要结构体数组

| 平行数组 | 结构体数组 |
|---|---|
| names[i], hp[i], atk[i] | Hero a[i] 整包 |
| 交换写 3 遍，易漏 | swap 一次 |

```cpp
struct Hero { string name; int hp, atk; };
Hero a[105];
swap(a[i], a[j]);  // 整包交换
```

---

## 2. sort 函数

```cpp
#include <algorithm>
sort(a, a + n);              // 数组默认升序
sort(a, a + n, greater<int>()); // 降序
sort(a + 1, a + n + 1, cmp);   // 从 1 开始 + 自定义
```

---

## 3. 自定义 cmp（裁判）

```cpp
bool cmp(类型 a, 类型 b) {
    return 条件;  // true → a 排 b 前面
}
```

**多关键字**：先比主键，相等再比次键。

```cpp
bool cmp(Person a, Person b) {
    if (a.vip != b.vip) return a.vip > b.vip;
    return a.arrive < b.arrive;
}
```

---

## 4. 经典题骨架

### P1502 成绩排序2

```cpp
struct Student { string name; int age, score; } a[1005];
bool cmp(Student x, Student y) { return x.score > y.score; }

int main() {
    int n; cin >> n;
    for (int i = 1; i <= n; i++)
        cin >> a[i].name >> a[i].age >> a[i].score;
    sort(a + 1, a + n + 1, cmp);
    for (int i = 1; i <= n; i++)
        cout << a[i].name << " " << a[i].age << " " << a[i].score << "\n";
}
```

### C5276 采购奖品（贪心+结构体）

```cpp
struct Goods { int price, num; } a[10005];
bool cmp(Goods x, Goods y) { return x.price < y.price; }
// sort 后从便宜到贵，钱够全包，不够买能买的然后 break
```

---

## 5. 易错点

| 坑 | 正确 |
|---|---|
| cmp 参数类型写错 | 与 sort 元素类型一致 |
| 降序写成 `a < b` | 要 `a.score > b.score` |
| 1-index 数组 | sort(a+1, a+n+1) |
| char name[] 用 = 赋值 | strcpy 或改 string |
| 大括号初始化顺序 | 按成员定义顺序 |

---

## 6. 题单

1. **基础**：`Point{x,y}` 按 x 降序，x 相同比 y 升序。  
2. **成绩表**：P1502，按成绩降序输出。  
3. **VIP 排队**：`Person{vip,arrive}`，VIP 高优先，同级先来先排。  
4. **采购**：C5276，价格升序贪心购买。  
5. **图书**：`Book{title,price,year}`，价格升序，相同则出版年升序。  
6. **结构体查找**：按学号二分（先按 id 排序）。

### 思考题

7. cmp 返回 true 时，是「a 在前」还是「b 在前」？  
8. 为什么成绩排序要打包姓名年龄，而不是只排 score 数组？

---

## 7. 多关键字 VIP 加长演示

打开 **`vip-sort.html`**（同目录）：

- 6 人队伍，VIP0/1/2 混编  
- **插入式逐步比较**：取出 → 与左侧逐个 `cmp` → 后移 / 插入  
- 每次比较显示：VIP 不同 → 大的在前；相同 → 到达序号小的在前  
- 底部日志记录每一步裁判理由  
- 支持「下一步 / 自动播放 / 直接看结果」

课堂用法：easy_sort ③ tab 建立概念 → vip-sort 让学生喊「下一步」跟裁判。

---

## 8. 课堂流程

1. easy_sort ① 数组交换灾难（5′）  
2. ② sort 默认排队（8′）  
3. ③ cmp 裁判 VIP（10′）  
4. **vip-sort 加长逐步比较**（10′）  
5. 黑板默写 cmp + P1502（10′）  
6. ④ 成绩表演示（5′）  
7. 当堂题 1、2（10′）  
