---
layout: article
title: 6. ZigZag Conversion
key: 100014
category: LeetCode
tags: LeetCode
date: 2020-03-18 11:15:00 +08:00
---

ZigZag Conversion

比较简单的题


# Brute Force

最简单，暴力搜索，时间复杂度是 $O(n^2)$

思想就是建个二维数组，然后按照规则遍历一遍字符串，更新数组，最后合并。

```c++
string convert(string s, int numRows) {
        //1. Brute Force
        if(s=="")
            return "";
        if(numRows == 1)
            return s;
        int str_len = s.length();
        char zig[numRows][str_len] = {};
        bool is_down = true;
        int x=0, y=0;
        for(int i = 0; i != str_len; i++){
            // cout << x << y << endl;
            if(is_down){
                zig[y][x]=s[i];
                if(y==numRows-1){
                    is_down = false;
                    x+=1;
                    if(y > 0)
                        y-=1;
                } else
                    y+=1;
            } else {
                zig[y][x]=s[i];
                if(y==0){
                    is_down = true;
                    y+=1;
                } else{
                    x+=1;
                    if(y > 0)
                        y-=1;
                }
            }
        }
        int ind=0;
        char restore_str[str_len+1];
        for(int r=0; r != numRows; r++)
            for(int j=0; j != str_len; j++){
                if(zig[r][j] != 0){
                    restore_str[ind] = zig[r][j];
                    ind++;
                }
            }
        restore_str[str_len] = '\0';
        return string(restore_str);
}
```



# Sort By Row

就是上述方法改进版，不需要后续遍历数组。

在虚拟state里进行遍历，按照顺序对每行进行append。

最后只需要加和。时间复杂度为$O(n)$

# Visit by row
很容易找到ZigZag的规律，按照规律进行append。时间复杂度也是$O(n)$

```C++
class Solution {
public:
    string longestPalindrome(string s) {
        // 2. Linear
        if(s=="")
            return "";
        if(numRows == 1)
            return s;
        int str_len = s.length();
        // cout << str_len;
        char restore_str[str_len+1];
        int mid_num = numRows - 2;
        int step_value = (numRows-2)*2 + 2;
        int ind = 0;
        for(int i = 0; i < str_len; i += step_value){
            restore_str[ind] = s[i];
            ind++;
            // cout << ind <<endl;
        }
        // cout << endl;
        for(int i = 0; i < mid_num; i++){
            int down = (numRows-3-i)*2 + 2;
            int up = i*2 + 2;
            bool flag = true;
            for(int j = i+1; j < str_len;){
                restore_str[ind] = s[j];
                ind++;
                // cout << j << endl;
                if(flag){
                    j+=down;
                    flag=false;
                } else {
                    j+=up;
                    flag=true;
                }
            }
        }
        // cout << endl;
        for(int i = numRows-1; i < str_len; i += step_value){
            restore_str[ind] = s[i];
            ind++;
            // cout << i << endl;
        }
        restore_str[ind] = '\0';
        return string(restore_str);
    }
};
```

