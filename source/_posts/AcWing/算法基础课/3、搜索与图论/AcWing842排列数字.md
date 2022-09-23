---
title: AcWing 842. 排列数字      
date: 
tags: 
	- Acwing 
	- DFS
categories: 
	- [AcWing,算法基础课,2、数据结构]
---

# AcWing 842. 排列数字    
### 题目来源--[842. 排列数字](https://www.acwing.com/problem/content/844/ "排列数字")

``` c++
题目描述
	给定一个整数 n，将数字 1∼n 排成一排，将会有很多种排列方法。
	现在，请你按照字典序将所有的排列方法输出。

输入格式
	共一行，包含一个整数 n。

输出格式
	按字典序输出所有排列方案，每个方案占一行。

数据范围
	1≤n≤7
	
输入样例：
	3
	
输出样例：
	1 2 3
	1 3 2
	2 1 3
	2 3 1
	3 1 2
	3 2 1	
```

## 代码演示

```c++
#include <iostream>

using namespace std;

const int N = 10;

int n;
int path[N];

void dfs(int u, int state)
{
    if (u == n)
    {
        for (int i = 0; i < n; i ++ ) printf("%d ", path[i]);
        puts("");

        return;
    }

    for (int i = 0; i < n; i ++ )
        if (!(state >> i & 1))
        {
            path[u] = i + 1;
            dfs(u + 1, state + (1 << i));
        }
}

int main()
{
    scanf("%d", &n);

    dfs(0, 0);

    return 0;
}

作者：yxc
链接：https://www.acwing.com/activity/content/code/content/47087/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

```