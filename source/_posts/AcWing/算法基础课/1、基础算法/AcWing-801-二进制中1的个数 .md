---
title: AcWing 801. 二进制中1的个数   
date: 
tags: 
	- Acwing 
	- 位运算
categories: 
	- [AcWing,算法基础课,1、基础算法]
---

# AcWing 801. 二进制中1的个数   
### 题目来源--[801. 二进制中1的个数](https://www.acwing.com/problem/content/803/ "判断子序列")

- - -
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
- - -
## 代码演示
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