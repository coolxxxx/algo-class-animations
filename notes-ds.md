# 数据结构题单（栈 / 队列 / 链表 / 二叉树）

配套：`?lesson=py6-1` `cpp6-4` `cpp6-6` `py5-7` `cpp5-8` `cpp6-9`  
VOX：`vox-stack` `vox-queue` `vox-linked` `vox-tree`

GESP 真题：https://gesp.ccf.org.cn/101/1010/index.html  
建议对照：五级链表、六级 STL stack/queue、树遍历。

---

## 1. 栈 · 括号匹配

```cpp
stack<char> st;
for (char c : s) {
    if (c=='(' || c=='[' || c=='{') st.push(c);
    else {
        if (st.empty()) { 不匹配; return; }
        char t = st.top(); st.pop();
        // 检查 t 与 c 是否配对
    }
}
if (!st.empty()) 不匹配;
```

题：`( [ ] ) ( )` 逐步画栈；`())(` 错在哪。

---

## 2. 队列 · BFS 底层

```cpp
queue<int> q;
q.push(1);          // 队尾
int x = q.front();  // 看队头
q.pop();            // 弹队头
```

题：对比 stack 后进先出；模拟排队 5 人报数。

---

## 3. 链表 · 改线不搬家

```cpp
// 数组模拟
int data[N], nxt[N], head;
// 删除值 x：找到前驱，nxt[pre] = nxt[cur]
```

题：  
1. 头插 3 个结点画图。  
2. 删除中间结点改哪条线。  
3. 删头结点特判。

---

## 4. 二叉树 · 前序

根→左→右。

```cpp
void pre(Node* p) {
    if (!p) return;
    cout << p->data;
    pre(p->left);
    pre(p->right);
}
```

题：画 A(B(D,E), C(F,G)) 前序序列；对照中序/后序（思考题）。

---

## 5. 课堂建议

每结构：VOX 5′ → 画图手推 → 骨架默写 → 一道 GESP 对照题。
