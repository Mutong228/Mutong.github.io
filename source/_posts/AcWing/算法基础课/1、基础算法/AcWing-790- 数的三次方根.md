---
title: AcWing 790. 数的三次方根
date: 
tags: 
	- Acwing 
	- 二分
categories: 
	- [AcWing,算法基础课,1、基础算法]
---

# AcWing 790. 数的三次方根 
### 题目来源--[790. 数的三次方根](https://www.acwing.com/problem/content/792/ "数的三次方根  ")

- - -
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
- - -
## 代码演示
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