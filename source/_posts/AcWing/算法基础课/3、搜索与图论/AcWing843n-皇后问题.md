---
title: AcWing 843. n-皇后问题       
date: 
tags: 
	- Acwing 
	- DFS
categories: 
	- [AcWing,算法基础课,2、数据结构]
---

# AcWing 843. n-皇后问题     
### 题目来源--[843. n-皇后问题](https://www.acwing.com/problem/content/844/ "n-皇后问题")

``` c++
题目描述
	n−皇后问题是指将 n 个皇后放在 n×n 的国际象棋棋盘上，使得皇后不能相互攻击到，即任意两个皇后都不能处于同一行、同一列或同一斜线上。
	现在给定整数 n，请你输出所有的满足条件的棋子摆法。

输入格式
	共一行，包含整数 n。

输出格式
	每个解决方案占 n 行，每行输出一个长度为 n 的字符串，用来表示完整的棋盘状态。
	其中 . 表示某一个位置的方格状态为空，Q 表示某一个位置的方格上摆着皇后。
	每个方案输出完成后，输出一个空行。
	注意：行末不能有多余空格。
	输出方案的顺序任意，只要不重复且没有遗漏即可。

数据范围
	1≤n≤9
	
输入样例：
	4
	
输出样例：
	.Q..
	...Q
	Q...
	..Q.

	..Q.
	Q...
	...Q
	.Q..
```
![图片](https://cdn.acwing.com/media/article/image/2019/06/08/19_860e00c489-1_597ec77c49-8-queens.png)

## 代码演示

```c++
#include <iostream>

using namespace std;

const int N = 10;

int n;
bool row[N], col[N], dg[N * 2], udg[N * 2];
char g[N][N];

void dfs(int x, int y, int s)
{
    if (s > n) return;
    if (y == n) y = 0, x ++ ;

    if (x == n)
    {
        if (s == n)
        {
            for (int i = 0; i < n; i ++ ) puts(g[i]);
            puts("");
        }
        return;
    }

    g[x][y] = '.';
    dfs(x, y + 1, s);

    if (!row[x] && !col[y] && !dg[x + y] && !udg[x - y + n])
    {
        row[x] = col[y] = dg[x + y] = udg[x - y + n] = true;
        g[x][y] = 'Q';
        dfs(x, y + 1, s + 1);
        g[x][y] = '.';
        row[x] = col[y] = dg[x + y] = udg[x - y + n] = false;
    }
}

int main()
{
    cin >> n;

    dfs(0, 0, 0);

    return 0;

作者：yxc
链接：https://www.acwing.com/activity/content/code/content/47097/
来源：AcWing
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```