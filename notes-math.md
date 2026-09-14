# 数论与位运算题单（GCD / 筛法 / 位 / 高精度 / 汉诺塔）

配套：`?lesson=cpp5-11` `py6-4` `cpp3-8` `cpp6-2` `py5-5`  
VOX：`vox-gcd` `vox-sieve` `vox-bits` `vox-bigadd` `vox-hanoi`

GESP 真题：https://gesp.ccf.org.cn/101/1010/index.html  
建议对照：三级位运算、五级 GCD/筛法、高精度。

---

## 1. 辗转相除

```cpp
int gcd(int a, int b) { return b ? gcd(b, a % b) : a; }
int lcm(int a, int b) { return a / gcd(a, b) * b; }
```

题：gcd(48,18)；gcd(17,5)；LCM(4,6)。

---

## 2. 埃氏筛

从 2 起关掉倍数；只筛到 √n。

题：30 以内质数个数（10）；100 以内（25）；为什么从 i*i 开始关。

---

## 3. 位运算

| 运算 | 含义 |
|---|---|
| n&1 | 判奇偶 |
| n<<1 | ×2 |
| n>>1 | ÷2 |
| a^b | 异或，可交换 |

题：  
1. 13 的二进制；13&1。  
2. 不用临时变量交换 a,b。  
3. `0b1010` 是几。

---

## 4. 高精度加法

倒序进数组，逐位加满十进一。

题：`123+879`；`999+1` 进位链；输出前去前导零。

---

## 5. 汉诺塔

n 个盘最少 2^n−1 步。

```cpp
void move(int n, char a, char c, char b) {
    if (n == 0) return;
    move(n-1, a, b, c);
    cout << a << "->" << c << endl;
    move(n-1, b, c, a);
}
```

题：n=3 数 7 步；n=4 多少（15）；参数顺序为什么是 a,c,b。

---

## 6. 易错

- gcd 递归忘 b=0 出口  
- LCM 先乘再除可能溢出 → `a/gcd*b`  
- 位运算优先级：`(n&1)==1` 要加括号
