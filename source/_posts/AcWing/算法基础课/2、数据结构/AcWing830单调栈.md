---
title: AcWing 830. 单调栈      
date: 
tags: 
	- Acwing 
	- 单调栈
categories: 
	- [AcWing,算法基础课,2、数据结构]
---

# AcWing 830. 单调栈    
### 题目来源--[830. 单调栈](https://www.acwing.com/problem/content/832/ "单调栈")

- - -
```c++

题目描述
	给定一个长度为 N 的整数数列，输出每个数左边第一个比它小的数，如果不存在则输出 −1。

输入格式
	第一行包含整数 N，表示数列长度。
	第二行包含 N 个整数，表示整数数列。

输出格式
	共一行，包含 N 个整数，其中第 i 个数表示第 i 个数的左边第一个比它小的数，如果不存在则输出 −1。

数据范围
	1≤N≤105
	1≤数列中元素≤109
	
输入样例：
	5
	3 4 2 7 5
	
输出样例：
	-1 3 -1 2 2

	
```
- - -
## 代码演示
```c++
#include <iostream>
using namespace std;
const int N = 100010;
int stk[N], tt;

int main()
{
    int n;
    cin >> n;
    while (n -- )
    {
        int x;
        scanf("%d", &x);
        while (tt && stk[tt] >= x) tt -- ;//如果栈顶元素大于当前待入栈元素，则出栈
        if (!tt) printf("-1 ");//如果栈空，则没有比该元素小的值。
        else printf("%d ", stk[tt]);//栈顶元素就是左侧第一个比它小的元素。
        stk[ ++ tt] = x;
    }
    return 0;
}

作者：Hasity
链接：https://www.acwing.com/solution/content/27437/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```