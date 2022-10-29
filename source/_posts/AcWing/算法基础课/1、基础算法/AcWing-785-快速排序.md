---
title: 基础算法
date: 
tags: 
	- Acwing 
categories: 
	- [AcWing,算法基础课,1、基础算法]
---

# AcWing 785. 快速排序

### 题目来源--[785. 快速排序](https://www.acwing.com/problem/content/787/ "快速排序")


```c++

题目描述：
    给定你一个长度为 n 的整数数列。
    请你使用快速排序对这个数列按照从小到大进行排序。
    并将排好序的数列按顺序输出。

输入格式
    输入共两行，第一行包含整数 n。
    第二行包含 n 个整数（所有整数均在 1∼109 范围内），表示整个数列。
	
输出格式
	输出共一行，包含 n 个整数，表示排好序的数列。

数据范围
	1≤n≤100000

输入样例：
    5
    3 1 2 4 5

输出样例：
    1 2 3 4 5
```
### 代码演示
```c++
#include <iostream>

using namespace std;

const int N = 100010;

int q[N];

void quick_sort(int q[], int l, int r)
{
    if (l >= r) return;

    int i = l - 1, j = r + 1, x = q[l + r >> 1];
    while (i < j)
    {
        do i ++ ; while (q[i] < x);
        do j -- ; while (q[j] > x);
        if (i < j) swap(q[i], q[j]);
    }

    quick_sort(q, l, j);
    quick_sort(q, j + 1, r);
}

int main()
{
    int n;
    scanf("%d", &n);

    for (int i = 0; i < n; i ++ ) scanf("%d", &q[i]);

    quick_sort(q, 0, n - 1);

    for (int i = 0; i < n; i ++ ) printf("%d ", q[i]);

    return 0;
}

作者：yxc
链接：https://www.acwing.com/activity/content/code/content/39784/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

- - -

# AcWing 786. 第k个数
### 题目来源--[786. 第k个数](https://www.acwing.com/problem/content/788/ "第k个数")

```c++

题目描述
	给定一个长度为 n 的整数数列，以及一个整数 k，请用快速选择算法求出数列从小到大排序后的第 k 个数。

输入格式
	第一行包含两个整数 n 和 k。
	第二行包含 n 个整数（所有整数均在 1～109 范围内），表示整数数列。

输出格式
	输出一个整数，表示数列的第 k 小数。

数据范围
	1≤n≤100000,
	1≤k≤n
输入样例：
	5 3
	2 4 1 5 3
输出样例：
	
```

### 代码演示
```c++
#include <iostream>

using namespace std;

const int N = 100010;

int q[N];

int quick_sort(int q[], int l, int r, int k)
{
    if (l >= r) return q[l];

    int i = l - 1, j = r + 1, x = q[l + r >> 1];
    while (i < j)
    {
        do i ++ ; while (q[i] < x);
        do j -- ; while (q[j] > x);
        if (i < j) swap(q[i], q[j]);
    }

    if (j - l + 1 >= k) return quick_sort(q, l, j, k);
    else return quick_sort(q, j + 1, r, k - (j - l + 1));
}

int main()
{
    int n, k;
    scanf("%d%d", &n, &k);

    for (int i = 0; i < n; i ++ ) scanf("%d", &q[i]);

    cout << quick_sort(q, 0, n - 1, k) << endl;

    return 0;
}

作者：yxc
链接：https://www.acwing.com/activity/content/code/content/39785/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

- - -

# AcWing 787. 归并排序
### 题目来源--[787. 归并排序](https://www.acwing.com/problem/content/789/ "归并排序")

```c++

题目描述
	给定你一个长度为 n 的整数数列。
	请你使用归并排序对这个数列按照从小到大进行排序。
	并将排好序的数列按顺序输出。

输入格式
	输入共两行，第一行包含整数 n。
	第二行包含 n 个整数（所有整数均在 1∼109 范围内），表示整个数列。

输出格式
	输出共一行，包含 n 个整数，表示排好序的数列。

数据范围
	1≤n≤100000
	
输入样例：
	5
	3 1 2 4 5
	
输出样例：
	1 2 3 4 5
	
```
### 代码演示
```c++
#include <iostream>

using namespace std;

const int N = 1e5 + 10;

int a[N], tmp[N];

void merge_sort(int q[], int l, int r)
{
    if (l >= r) return;

    int mid = l + r >> 1;

    merge_sort(q, l, mid), merge_sort(q, mid + 1, r);

    int k = 0, i = l, j = mid + 1;
    while (i <= mid && j <= r)
        if (q[i] <= q[j]) tmp[k ++ ] = q[i ++ ];
        else tmp[k ++ ] = q[j ++ ];
    while (i <= mid) tmp[k ++ ] = q[i ++ ];
    while (j <= r) tmp[k ++ ] = q[j ++ ];

    for (i = l, j = 0; i <= r; i ++, j ++ ) q[i] = tmp[j];
}

int main()
{
    int n;
    scanf("%d", &n);
    for (int i = 0; i < n; i ++ ) scanf("%d", &a[i]);

    merge_sort(a, 0, n - 1);

    for (int i = 0; i < n; i ++ ) printf("%d ", a[i]);

    return 0;
}

作者：yxc
链接：https://www.acwing.com/activity/content/code/content/39790/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```
- - -

# AcWing 788. 逆序对的数量

### 题目来源--[788. 逆序对的数量](https://www.acwing.com/problem/content/790/ "逆序对的数量 ")

```c++

题目描述
	给定一个长度为 n 的整数数列，请你计算数列中的逆序对的数量。
	逆序对的定义如下：对于数列的第 i 个和第 j 个元素，如果满足 i<j 且 a[i]>a[j]，则其为一个逆序对；否则不是。

输入格式
	第一行包含整数 n，表示数列的长度。
	第二行包含 n 个整数，表示整个数列。

输出格式
	输出一个整数，表示逆序对的个数。

数据范围
	1≤n≤100000，
	
数列中的元素的取值范围 [1,109]。

输入样例：
	6
	2 3 4 5 6 1
	
输出样例：
	5
	
```

### 代码演示
```c++
#include <iostream>

using namespace std;

typedef long long LL;

const int N = 1e5 + 10;

int a[N], tmp[N];

LL merge_sort(int q[], int l, int r)
{
    if (l >= r) return 0;

    int mid = l + r >> 1;

    LL res = merge_sort(q, l, mid) + merge_sort(q, mid + 1, r);

    int k = 0, i = l, j = mid + 1;
    while (i <= mid && j <= r)
        if (q[i] <= q[j]) tmp[k ++ ] = q[i ++ ];
        else
        {
            res += mid - i + 1;
            tmp[k ++ ] = q[j ++ ];
        }
    while (i <= mid) tmp[k ++ ] = q[i ++ ];
    while (j <= r) tmp[k ++ ] = q[j ++ ];

    for (i = l, j = 0; i <= r; i ++, j ++ ) q[i] = tmp[j];

    return res;
}

int main()
{
    int n;
    scanf("%d", &n);
    for (int i = 0; i < n; i ++ ) scanf("%d", &a[i]);

    cout << merge_sort(a, 0, n - 1) << endl;

    return 0;
}

作者：yxc
链接：https://www.acwing.com/activity/content/code/content/39791/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

- - -

# AcWing 789. 数的范围

### 题目来源--[789. 数的范围](https://www.acwing.com/problem/content/791/ "数的范围  ")

```c++

题目描述
	给定一个按照升序排列的长度为 n 的整数数组，以及 q 个查询。
	对于每个查询，返回一个元素 k 的起始位置和终止位置（位置从 0 开始计数）。
	如果数组中不存在该元素，则返回 -1 -1。

输入格式
	第一行包含整数 n 和 q，表示数组长度和询问个数。
	第二行包含 n 个整数（均在 1～10000 范围内），表示完整数组。
	接下来 q 行，每行包含一个整数 k，表示一个询问元素。

输出格式
	共 q 行，每行包含两个整数，表示所求元素的起始位置和终止位置。
	如果数组中不存在该元素，则返回 -1 -1。

数据范围
	1≤n≤100000
	1≤q≤10000
	1≤k≤10000
	
输入样例：
	6 3
	1 2 2 3 3 4
	3
	4
	5
	
输出样例：
	3 4
	5 5
	-1 -1
	
```

### 代码演示
```c++
#include <iostream>

using namespace std;

const int N = 100010;

int n, m;
int q[N];

int main()
{
    scanf("%d%d", &n, &m);
    for (int i = 0; i < n; i ++ ) scanf("%d", &q[i]);

    while (m -- )
    {
        int x;
        scanf("%d", &x);

        int l = 0, r = n - 1;
        while (l < r)
        {
            int mid = l + r >> 1;
            if (q[mid] >= x) r = mid;
            else l = mid + 1;
        }

        if (q[l] != x) cout << "-1 -1" << endl;
        else
        {
            cout << l << ' ';

            int l = 0, r = n - 1;
            while (l < r)
            {
                int mid = l + r + 1 >> 1;
                if (q[mid] <= x) l = mid;
                else r = mid - 1;
            }

            cout << l << endl;
        }
    }

    return 0;
}

作者：yxc
链接：https://www.acwing.com/activity/content/code/content/39787/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

- - -

# AcWing 790. 数的三次方根 

### 题目来源--[790. 数的三次方根](https://www.acwing.com/problem/content/792/ "数的三次方根  ")

```c++

题目描述
	给定一个浮点数 n，求它的三次方根。

输入格式
	共一行，包含一个浮点数 n。

输出格式
	共一行，包含一个浮点数，表示问题的解。
	注意，结果保留 6 位小数。

数据范围
	-10000≤n≤10000
	
输入样例：
	1000.00
	
输出样例：
	10.000000
	
```

### 代码演示
```c++
#include <iostream>

using namespace std;

int main()
{
    double x;
    cin >> x;

    double l = -100, r = 100;
    while (r - l > 1e-8)
    {
        double mid = (l + r) / 2;
        if (mid * mid * mid >= x) r = mid;
        else l = mid;
    }

    printf("%.6lf\n", l);
    return 0;
}
```

- - -

# AcWing 791. 高精度加法 

### 题目来源--[791.高精度加法](https://www.acwing.com/problem/content/793/"高精度加法")

```c++

题目描述
	给定两个正整数（不含前导 0），计算它们的和。

输入格式
	共两行，每行包含一个整数。

输出格式
	共一行，包含所求的和。

数据范围
	1≤整数长度≤100000
输入样例：

	12
	23
	
输出样例：
	35
	
```

## 不圧位代码
```c++
#include <iostream>
#include <vector>

using namespace std;

vector<int> add(vector<int> &A, vector<int> &B)
{
    if (A.size() < B.size()) return add(B, A);

    vector<int> C;
    int t = 0;
    for (int i = 0; i < A.size(); i ++ )
    {
        t += A[i];
        if (i < B.size()) t += B[i];
        C.push_back(t % 10);
        t /= 10;
    }

    if (t) C.push_back(t);
    return C;
}

int main()
{
    string a, b;
    vector<int> A, B;
    cin >> a >> b;
    for (int i = a.size() - 1; i >= 0; i -- ) A.push_back(a[i] - '0');
    for (int i = b.size() - 1; i >= 0; i -- ) B.push_back(b[i] - '0');

    auto C = add(A, B);

    for (int i = C.size() - 1; i >= 0; i -- ) cout << C[i];
    cout << endl;

    return 0;
}

作者：yxc
链接：https://www.acwing.com/activity/content/code/content/39792/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

## 压9位的代码

```C++
#include <iostream>
#include <vector>

using namespace std;

const int base = 1000000000;

vector<int> add(vector<int> &A, vector<int> &B)
{
    if (A.size() < B.size()) return add(B, A);

    vector<int> C;
    int t = 0;
    for (int i = 0; i < A.size(); i ++ )
    {
        t += A[i];
        if (i < B.size()) t += B[i];
        C.push_back(t % base);
        t /= base;
    }

    if (t) C.push_back(t);
    return C;
}

int main()
{
    string a, b;
    vector<int> A, B;
    cin >> a >> b;

    for (int i = a.size() - 1, s = 0, j = 0, t = 1; i >= 0; i -- )
    {
        s += (a[i] - '0') * t;
        j ++, t *= 10;
        if (j == 9 || i == 0)
        {
            A.push_back(s);
            s = j = 0;
            t = 1;
        }
    }
    for (int i = b.size() - 1, s = 0, j = 0, t = 1; i >= 0; i -- )
    {
        s += (b[i] - '0') * t;
        j ++, t *= 10;
        if (j == 9 || i == 0)
        {
            B.push_back(s);
            s = j = 0;
            t = 1;
        }
    }

    auto C = add(A, B);

    cout << C.back();
    for (int i = C.size() - 2; i >= 0; i -- ) printf("%09d", C[i]);
    cout << endl;

    return 0;
}

作者：yxc
链接：https://www.acwing.com/activity/content/code/content/39792/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

- - -

# AcWing 792. 高精度减法 

### 题目来源--[792. 高精度减法 ](https://www.acwing.com/problem/content/794/ "高精度减法")

```c++

题目描述
	给定两个正整数（不含前导 0），计算它们的差，计算结果可能为负数。

输入格式
	共两行，每行包含一个整数。

输出格式
	共一行，包含所求的差。

数据范围
	1≤整数长度≤105
	
输入样例：
	32
	11
	
输出样例：
	21
	
```

### 代码演示
```c++
#include <iostream>
#include <vector>

using namespace std;

bool cmp(vector<int> &A, vector<int> &B)
{
    if (A.size() != B.size()) return A.size() > B.size();

    for (int i = A.size() - 1; i >= 0; i -- )
        if (A[i] != B[i])
            return A[i] > B[i];

    return true;
}

vector<int> sub(vector<int> &A, vector<int> &B)
{
    vector<int> C;
    for (int i = 0, t = 0; i < A.size(); i ++ )
    {
        t = A[i] - t;
        if (i < B.size()) t -= B[i];
        C.push_back((t + 10) % 10);
        if (t < 0) t = 1;
        else t = 0;
    }

    while (C.size() > 1 && C.back() == 0) C.pop_back();
    return C;
}

int main()
{
    string a, b;
    vector<int> A, B;
    cin >> a >> b;
    for (int i = a.size() - 1; i >= 0; i -- ) A.push_back(a[i] - '0');
    for (int i = b.size() - 1; i >= 0; i -- ) B.push_back(b[i] - '0');

    vector<int> C;

    if (cmp(A, B)) C = sub(A, B);
    else C = sub(B, A), cout << '-';

    for (int i = C.size() - 1; i >= 0; i -- ) cout << C[i];
    cout << endl;

    return 0;
}

作者：yxc
链接：https://www.acwing.com/activity/content/code/content/39793/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

- - -

# AcWing 793. 高精度乘法

### 题目来源--[793. 高精度乘法](https://www.acwing.com/problem/content/795/ "高精度乘法")

```c++

题目描述
	给定两个非负整数（不含前导 0） A 和 B，请你计算 A×B 的值。

输入格式
	共两行，第一行包含整数 A，第二行包含整数 B。

输出格式
	共一行，包含 A×B 的值。

数据范围
	1≤A的长度≤100000,
	0≤B≤10000
	
输入样例：
	2
	3
	
输出样例：
	6
	
```

### 代码演示
```c++
#include <iostream>
#include <vector>

using namespace std;


vector<int> mul(vector<int> &A, int b)
{
    vector<int> C;

    int t = 0;
    for (int i = 0; i < A.size() || t; i ++ )
    {
        if (i < A.size()) t += A[i] * b;
        C.push_back(t % 10);
        t /= 10;
    }

    while (C.size() > 1 && C.back() == 0) C.pop_back();

    return C;
}


int main()
{
    string a;
    int b;

    cin >> a >> b;

    vector<int> A;
    for (int i = a.size() - 1; i >= 0; i -- ) A.push_back(a[i] - '0');

    auto C = mul(A, b);

    for (int i = C.size() - 1; i >= 0; i -- ) printf("%d", C[i]);

    return 0;
}

作者：yxc
链接：https://www.acwing.com/activity/content/code/content/39794/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

- - -

# AcWing 794. 高精度除法  

### 题目来源--[794. 高精度除法](https://www.acwing.com/problem/content/796/ "高精度除法")

```c++

题目描述
	给定两个非负整数（不含前导 0） A，B，请你计算 A/B 的商和余数。

输入格式
	共两行，第一行包含整数 A，第二行包含整数 B。

输出格式
	共两行，第一行输出所求的商，第二行输出所求余数。

数据范围
	1≤A的长度≤100000,
	1≤B≤10000,
	B 一定不为 0
	
输入样例：
	7
	2
	
输出样例：
	3
	1
	
```

### 代码演示
```c++
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> div(vector<int> &A, int b, int &r)
{
    vector<int> C;
    r = 0;
    for (int i = A.size() - 1; i >= 0; i -- )
    {
        r = r * 10 + A[i];
        C.push_back(r / b);
        r %= b;
    }
    reverse(C.begin(), C.end());
    while (C.size() > 1 && C.back() == 0) C.pop_back();
    return C;
}

int main()
{
    string a;
    vector<int> A;

    int B;
    cin >> a >> B;
    for (int i = a.size() - 1; i >= 0; i -- ) A.push_back(a[i] - '0');

    int r;
    auto C = div(A, B, r);

    for (int i = C.size() - 1; i >= 0; i -- ) cout << C[i];

    cout << endl << r << endl;

    return 0;
}

作者：yxc
链接：https://www.acwing.com/activity/content/code/content/39795/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

- - -

# AcWing 795. 前缀和   

### 题目来源--[795. 前缀和](https://www.acwing.com/problem/content/797/ "前缀和")

```c++

题目描述
	输入一个长度为 n 的整数序列。
	接下来再输入 m 个询问，每个询问输入一对 l,r。
	对于每个询问，输出原序列中从第 l 个数到第 r 个数的和。

输入格式
	第一行包含两个整数 n 和 m。
	第二行包含 n 个整数，表示整数数列。
	接下来 m 行，每行包含两个整数 l 和 r，表示一个询问的区间范围。

输出格式
	共 m 行，每行输出一个询问的结果。

数据范围
	1≤l≤r≤n,
	1≤n,m≤100000,
	−1000≤数列中元素的值≤1000
	
输入样例：
	5 3
	2 1 3 6 4
	1 2
	1 3
	2 4
	
输出样例：
	3
	6
	10
	
```

### 代码演示
```c++
#include <iostream>

using namespace std;

const int N = 100010;

int n, m;
int a[N], s[N];

int main()
{
    scanf("%d%d", &n, &m);
    for (int i = 1; i <= n; i ++ ) scanf("%d", &a[i]);

    for (int i = 1; i <= n; i ++ ) s[i] = s[i - 1] + a[i]; // 前缀和的初始化

    while (m -- )
    {
        int l, r;
        scanf("%d%d", &l, &r);
        printf("%d\n", s[r] - s[l - 1]); // 区间和的计算
    }

    return 0;
}

作者：yxc
链接：https://www.acwing.com/activity/content/code/content/39796/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

- - -

# AcWing 796. 子矩阵的和 
  
### 题目来源--[796. 子矩阵的和](https://www.acwing.com/problem/content/798/ "子矩阵的和")

```c++

题目描述
	输入一个 n 行 m 列的整数矩阵，再输入 q 个询问，每个询问包含四个整数 x1,y1,x2,y2，表示一个子矩阵的左上角坐标和右下角坐标。
	对于每个询问输出子矩阵中所有数的和。

输入格式
	第一行包含三个整数 n，m，q。
	接下来 n 行，每行包含 m 个整数，表示整数矩阵。
	接下来 q 行，每行包含四个整数 x1,y1,x2,y2，表示一组询问。

输出格式
	共 q 行，每行输出一个询问的结果。

数据范围
	1≤n,m≤1000,
	1≤q≤200000,
	1≤x1≤x2≤n,
	1≤y1≤y2≤m,
	−1000≤矩阵内元素的值≤1000
	
输入样例：
	3 4 3
	1 7 2 4
	3 6 2 8
	2 1 2 3
	1 1 2 2
	2 1 3 4
	1 3 3 4
	
输出样例：
	17
	27
	21
	
```

### 代码演示
```c++
#include <iostream>

using namespace std;

const int N = 1010;

int n, m, q;
int s[N][N];

int main()
{
    scanf("%d%d%d", &n, &m, &q);

    for (int i = 1; i <= n; i ++ )
        for (int j = 1; j <= m; j ++ )
            scanf("%d", &s[i][j]);

    for (int i = 1; i <= n; i ++ )
        for (int j = 1; j <= m; j ++ )
            s[i][j] += s[i - 1][j] + s[i][j - 1] - s[i - 1][j - 1];

    while (q -- )
    {
        int x1, y1, x2, y2;
        scanf("%d%d%d%d", &x1, &y1, &x2, &y2);
        printf("%d\n", s[x2][y2] - s[x1 - 1][y2] - s[x2][y1 - 1] + s[x1 - 1][y1 - 1]);
    }

    return 0;
}

作者：yxc
链接：https://www.acwing.com/activity/content/code/content/39797/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

- - -

# AcWing 797. 差分   

### 题目来源--[797. 差分](https://www.acwing.com/problem/content/799/ "差分")

```c++

题目描述
	输入一个长度为 n 的整数序列。
	接下来输入 m 个操作，每个操作包含三个整数 l,r,c，表示将序列中 [l,r] 之间的每个数加上 c。
	请你输出进行完所有操作后的序列。

输入格式
	第一行包含两个整数 n 和 m。
	第二行包含 n 个整数，表示整数序列。
	接下来 m 行，每行包含三个整数 l，r，c，表示一个操作。

输出格式
	共一行，包含 n 个整数，表示最终序列。

数据范围
	1≤n,m≤100000,
	1≤l≤r≤n,
	−1000≤c≤1000,
	−1000≤整数序列中元素的值≤1000
	
输入样例：
	6 3
	1 2 2 1 2 1
	1 3 1
	3 5 1
	1 6 1
	
输出样例：
	3 4 5 3 4 2
	
```

### 代码演示
```c++
#include <iostream>

using namespace std;

const int N = 100010;

int n, m;
int a[N], b[N];

void insert(int l, int r, int c)
{
    b[l] += c;
    b[r + 1] -= c;
}

int main()
{
    scanf("%d%d", &n, &m);
    for (int i = 1; i <= n; i ++ ) scanf("%d", &a[i]);

    for (int i = 1; i <= n; i ++ ) insert(i, i, a[i]);

    while (m -- )
    {
        int l, r, c;
        scanf("%d%d%d", &l, &r, &c);
        insert(l, r, c);
    }

    for (int i = 1; i <= n; i ++ ) b[i] += b[i - 1];

    for (int i = 1; i <= n; i ++ ) printf("%d ", b[i]);

    return 0;
}

作者：yxc
链接：https://www.acwing.com/activity/content/code/content/39799/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

- - -

# AcWing 798. 差分矩阵
   
### 题目来源--[798. 差分矩阵](https://www.acwing.com/problem/content/800/ "差分")

```c++

题目描述
	输入一个 n 行 m 列的整数矩阵，再输入 q 个操作，每个操作包含五个整数 x1,y1,x2,y2,c，其中 (x1,y1) 和 (x2,y2) 表示一个子矩阵的左上角坐标和右下角坐标。
	每个操作都要将选中的子矩阵中的每个元素的值加上 c。
	请你将进行完所有操作后的矩阵输出。

输入格式
	第一行包含整数 n,m,q。
	接下来 n 行，每行包含 m 个整数，表示整数矩阵。
	接下来 q 行，每行包含 5 个整数 x1,y1,x2,y2,c，表示一个操作。

输出格式
	共 n 行，每行 m 个整数，表示所有操作进行完毕后的最终矩阵。

数据范围
	1≤n,m≤1000,
	1≤q≤100000,
	1≤x1≤x2≤n,
	1≤y1≤y2≤m,
	−1000≤c≤1000,
	−1000≤矩阵内元素的值≤1000
	
输入样例：
	3 4 3
	1 2 2 1
	3 2 2 1
	1 1 1 1
	1 1 2 2 1
	1 3 2 3 2
	3 1 3 4 1
	
输出样例：
	2 3 4 1
	4 3 4 1
	2 2 2 2
	
```

### 代码演示
```c++
#include <iostream>

using namespace std;

const int N = 1010;

int n, m, q;
int a[N][N], b[N][N];

void insert(int x1, int y1, int x2, int y2, int c)
{
    b[x1][y1] += c;
    b[x2 + 1][y1] -= c;
    b[x1][y2 + 1] -= c;
    b[x2 + 1][y2 + 1] += c;
}

int main()
{
    scanf("%d%d%d", &n, &m, &q);

    for (int i = 1; i <= n; i ++ )
        for (int j = 1; j <= m; j ++ )
            scanf("%d", &a[i][j]);

    for (int i = 1; i <= n; i ++ )
        for (int j = 1; j <= m; j ++ )
            insert(i, j, i, j, a[i][j]);

    while (q -- )
    {
        int x1, y1, x2, y2, c;
        cin >> x1 >> y1 >> x2 >> y2 >> c;
        insert(x1, y1, x2, y2, c);
    }

    for (int i = 1; i <= n; i ++ )
        for (int j = 1; j <= m; j ++ )
            b[i][j] += b[i - 1][j] + b[i][j - 1] - b[i - 1][j - 1];

    for (int i = 1; i <= n; i ++ )
    {
        for (int j = 1; j <= m; j ++ ) printf("%d ", b[i][j]);
        puts("");
    }

    return 0;
}


作者：yxc
链接：https://www.acwing.com/activity/content/code/content/39800/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

- - -

# AcWing 799. 最长连续不重复子序列  
 
### 题目来源--[799. 最长连续不重复子序列](https://www.acwing.com/problem/content/801/ "最长连续不重复子序列")


```c++

题目描述
	给定一个长度为 n 的整数序列，请找出最长的不包含重复的数的连续区间，输出它的长度。

输入格式
	第一行包含整数 n。
	第二行包含 n 个整数（均在 0∼105 范围内），表示整数序列。

输出格式
	共一行，包含一个整数，表示最长的不包含重复的数的连续区间的长度。

数据范围
	1≤n≤105
	
输入样例：
	5
	1 2 2 3 5
	
输出样例：
	3
	
```

### 代码演示
```c++
#include <iostream>

using namespace std;

const int N = 100010;

int n;
int q[N], s[N];

int main()
{
    scanf("%d", &n);
    for (int i = 0; i < n; i ++ ) scanf("%d", &q[i]);

    int res = 0;
    for (int i = 0, j = 0; i < n; i ++ )
    {
        s[q[i]] ++ ;
        while (j < i && s[q[i]] > 1) s[q[j ++ ]] -- ;
        res = max(res, i - j + 1);
    }

    cout << res << endl;

    return 0;
}

作者：yxc
链接：https://www.acwing.com/activity/content/code/content/40066/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

- - -

# AcWing 800. 数组元素的目标和   

### 题目来源--[800. 数组元素的目标和](https://www.acwing.com/problem/content/802/ "数组元素的目标和")

```c++

题目描述
	给定两个升序排序的有序数组 A 和 B，以及一个目标值 x。
	数组下标从 0 开始。
	请你求出满足 A[i]+B[j]=x 的数对 (i,j)。
	数据保证有唯一解。

输入格式
	第一行包含三个整数 n,m,x，分别表示 A 的长度，B 的长度以及目标值 x。
	第二行包含 n 个整数，表示数组 A。
	第三行包含 m 个整数，表示数组 B。

输出格式
	共一行，包含两个整数 i 和 j。

数据范围
	数组长度不超过 105。
	同一数组内元素各不相同。
	1≤数组元素≤109
	
输入样例：
	4 5 6
	1 2 4 7
	3 4 6 8 9
	
输出样例：
	1 1
	
```

### 代码演示
```c++
#include <iostream>

using namespace std;

const int N = 1e5 + 10;

int n, m, x;
int a[N], b[N];

int main()
{
    scanf("%d%d%d", &n, &m, &x);
    for (int i = 0; i < n; i ++ ) scanf("%d", &a[i]);
    for (int i = 0; i < m; i ++ ) scanf("%d", &b[i]);

    for (int i = 0, j = m - 1; i < n; i ++ )
    {
        while (j >= 0 && a[i] + b[j] > x) j -- ;
        if (j >= 0 && a[i] + b[j] == x) cout << i << ' ' << j << endl;
    }

    return 0;
}

作者：yxc
链接：https://www.acwing.com/activity/content/code/content/40069/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

- - -

# AcWing 801. 二进制中1的个数   

### 题目来源--[801. 二进制中1的个数](https://www.acwing.com/problem/content/803/ "判断子序列")

```c++

题目描述
	给定一个长度为 n 的数列，请你求出数列中每个数的二进制表示中 1 的个数。

输入格式
	第一行包含整数 n。
	第二行包含 n 个整数，表示整个数列。

输出格式
	共一行，包含 n 个整数，其中的第 i 个数表示数列中的第 i 个数的二进制表示中 1 的个数。

数据范围
	1≤n≤100000,
	0≤数列中元素的值≤109
	
输入样例：
	5
	1 2 3 4 5
	
输出样例：
	1 1 2 1 2

	
```

### 代码演示
```c++
#include <iostream>

using namespace std;

int main()
{
    int n;
    scanf("%d", &n);
    while (n -- )
    {
        int x, s = 0;
        scanf("%d", &x);

        for (int i = x; i; i -= i & -i) s ++ ;

        printf("%d ", s);
    }

    return 0;
}
```

- - -

# AcWing 802. 区间和   
 
### 题目来源--[802. 区间和](https://www.acwing.com/problem/content/804/ "区间和")

```c++

题目描述
	假定有一个无限长的数轴，数轴上每个坐标上的数都是 0。
	现在，我们首先进行 n 次操作，每次操作将某一位置 x 上的数加 c。
	接下来，进行 m 次询问，每个询问包含两个整数 l 和 r，你需要求出在区间 [l,r] 之间的所有数的和。

输入格式
	第一行包含两个整数 n 和 m。
	接下来 n 行，每行包含两个整数 x 和 c。
	再接下来 m 行，每行包含两个整数 l 和 r。

输出格式
	共 m 行，每行输出一个询问中所求的区间内数字和。

数据范围
	−109≤x≤109,
	1≤n,m≤105,
	−109≤l≤r≤109,
	−10000≤c≤10000
	
输入样例：
	3 3
	1 2
	3 6
	7 5
	1 3
	4 6
	7 8
	
输出样例：
	8
	0
	5

	
```

### 代码演示
```c++
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

typedef pair<int, int> PII;

const int N = 300010;

int n, m;
int a[N], s[N];

vector<int> alls;
vector<PII> add, query;

int find(int x)
{
    int l = 0, r = alls.size() - 1;
    while (l < r)
    {
        int mid = l + r >> 1;
        if (alls[mid] >= x) r = mid;
        else l = mid + 1;
    }
    return r + 1;
}

int main()
{
    cin >> n >> m;
    for (int i = 0; i < n; i ++ )
    {
        int x, c;
        cin >> x >> c;
        add.push_back({x, c});

        alls.push_back(x);
    }

    for (int i = 0; i < m; i ++ )
    {
        int l, r;
        cin >> l >> r;
        query.push_back({l, r});

        alls.push_back(l);
        alls.push_back(r);
    }

    // 去重
    sort(alls.begin(), alls.end());
    alls.erase(unique(alls.begin(), alls.end()), alls.end());

    // 处理插入
    for (auto item : add)
    {
        int x = find(item.first);
        a[x] += item.second;
    }

    // 预处理前缀和
    for (int i = 1; i <= alls.size(); i ++ ) s[i] = s[i - 1] + a[i];

    // 处理询问
    for (auto item : query)
    {
        int l = find(item.first), r = find(item.second);
        cout << s[r] - s[l - 1] << endl;
    }

    return 0;
}

作者：yxc
链接：https://www.acwing.com/activity/content/code/content/40105/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

- - -

# AcWing 2816. 判断子序列   

### 题目来源--[2816. 判断子序列](https://www.acwing.com/problem/content/2818/ "判断子序列")

```c++

题目描述
	给定一个长度为 n 的整数序列 a1,a2,…,an 以及一个长度为 m 的整数序列 b1,b2,…,bm。
	请你判断 a 序列是否为 b 序列的子序列。
	子序列指序列的一部分项按原有次序排列而得的序列，例如序列 {a1,a3,a5} 是序列 {a1,a2,a3,a4,a5} 的一个子序列。

输入格式
	第一行包含两个整数 n,m。
	第二行包含 n 个整数，表示 a1,a2,…,an。
	第三行包含 m 个整数，表示 b1,b2,…,bm。

输出格式
	如果 a 序列是 b 序列的子序列，输出一行 Yes。
	否则，输出 No。

数据范围
	1≤n≤m≤105,
	−109≤ai,bi≤109
	
输入样例：
	3 5
	1 3 5
	1 2 3 4 5
	
输出样例：
	Yes

	
```

### 代码演示
```c++
#include <iostream>
#include <cstring>

using namespace std;

const int N = 100010;

int n, m;
int a[N], b[N];

int main()
{
    scanf("%d%d", &n, &m);
    for (int i = 0; i < n; i ++ ) scanf("%d", &a[i]);
    for (int i = 0; i < m; i ++ ) scanf("%d", &b[i]);

    int i = 0, j = 0;
    while (i < n && j < m)
    {
        if (a[i] == b[j]) i ++ ;
        j ++ ;
    }

    if (i == n) puts("Yes");
    else puts("No");

    return 0;
}

作者：yxc
链接：https://www.acwing.com/activity/content/code/content/589289/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```