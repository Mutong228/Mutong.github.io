---
title: AcWing 838. 堆排序      
date: 
tags: 
	- Acwing 
	- 堆
categories: 
	- [AcWing,算法基础课,2、数据结构]
---

# AcWing 838. 堆排序    
### 题目来源--[838. 堆排序](https://www.acwing.com/problem/content/840/ "堆排序")

``` c++
题目描述
	输入一个长度为 n 的整数数列，从小到大输出前 m 小的数。

输入格式
	第一行包含整数 n 和 m。
	第二行包含 n 个整数，表示整数数列。

输出格式
	共一行，包含 m 个整数，表示整数数列中前 m 小的数。

数据范围
	1≤m≤n≤105，
	1≤数列中元素≤109
	
输入样例：
	5 3
	4 5 1 3 2
	
输出样例：
	1 2 3
	
```

## 代码演示
```c++
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 100010;

int n, m;
int h[N], cnt;

void down(int u)
{
    int t = u;
    if (u * 2 <= cnt && h[u * 2] < h[t]) t = u * 2;
    if (u * 2 + 1 <= cnt && h[u * 2 + 1] < h[t]) t = u * 2 + 1;
    if (u != t)
    {
        swap(h[u], h[t]);
        down(t);
    }
}

int main()
{
    scanf("%d%d", &n, &m);
    for (int i = 1; i <= n; i ++ ) scanf("%d", &h[i]);
    cnt = n;

    for (int i = n / 2; i; i -- ) down(i);

    while (m -- )
    {
        printf("%d ", h[1]);
        h[1] = h[cnt -- ];
        down(1);
    }

    puts("");

    return 0;
}

作者：yxc
链接：https://www.acwing.com/activity/content/code/content/45296/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```