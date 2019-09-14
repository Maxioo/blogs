---
layout: article
title: POJ 2386 Lake Counting
key: 100009
category: blog
tags: POJ
date: 2019-09-14 16:55:00 +08:00
modify_date: 2019-09-14 16:55:00 +08:00
---

# 1. 问题简介

POJ ID 2386，简单的dfs问题。

# 2. 思路

对每个单元进行遍历，如果发现'W'，则进行递归填充周边8个区域，直到不能填充位置。

进行dfs的次数即为问题答案。

# 3. Code

```C++
#include<iostream>
#include<fstream>

const int DEBUG = 0;
const int MAXNM = 100;

char all_temp[MAXNM][MAXNM] = {0};
void dfs(int n_site, int m_site, int N, int M){
    all_temp[n_site][m_site] = '.';
    for(int i = -1; i <=1; i++)
        for(int j = -1; j <= 1; j++){
            if(n_site + i < 0 | n_site + i >= N | m_site + j < 0 | m_site + j >= M)
                continue;
            if(all_temp[n_site+i][m_site+j] == 'W')
                dfs(n_site+i,m_site+j,N,M);
        }
}

void solve()
{
    if(DEBUG){
        std::ifstream fin("input");
        std::streambuf *cinbackup;
        cinbackup = std::cin.rdbuf(fin.rdbuf());
    }

    int N, M;
    std::cin >> N >> M;

    char temp_char;
    for(int i = 0; i != N; i++)
        for(int j = 0; j != M; j++){
            std::cin >> temp_char;
            all_temp[i][j] = temp_char;
        }
    int count = 0;
    for(int i = 0; i != N; i++)
        for(int j = 0; j != M; j++){
            if(all_temp[i][j] == 'W'){
                dfs(i, j, N, M);
                count++;
            }
        }
    std::cout << count << std::endl;
}

int main()
{
    solve();
}
```