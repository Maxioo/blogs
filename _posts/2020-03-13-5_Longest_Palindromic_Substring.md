---
layout: article
title: 5. Longest Palindromic Substring
key: 100013
category: LeetCode
tags: LeetCode
date: 2020-03-13 09:18:00 +08:00
---

Longest Palindromic Substring

最长回文子串，应该是最经典的题目了。


# Brute Force

最简单，暴力搜索，时间复杂度是 $O(n^3)$

代码很简单，不贴。

# Dynamic Programming

动态规划，将一些state缓存以减小时间消耗。

令$P(i,j)$为状态，值为0代表substr(i,j)不是回文串，值大于0则代表是回文串，且值代表子串长度。
$$
P(i,j)
\begin{cases}
1, &&if&i==j.\\
2, &&if&str[i]==str[j].\\
P(i+1,j-1)+2, &&if&P(i+1,j-1)>0\&\&str[i]==str[j].
\end{cases}
$$


时间复杂度是$O(n^2)$，空间复杂度是$O(n^2)$，可进一步优化成$O(n)$，具体是一行状态的计算只依赖于上一行，所以保存两行状态即可。

```C++
class Solution {
public:
    string longestPalindrome(string s) {
        int lens = s.length();
        if(lens == 0)
            return "";
        int status[lens][lens] = {};
        int left = 0, right = 0;
        for(int i = 0; i < lens; i++){
            for(left = 0; left < lens - i; left++){
                right = left + i;
                if(i == 0)
                    status[left][right] = 1;
                else if (i == 1 && s[left] == s[right])
                    status[left][right] = 2;
                else{
                    if(status[left+1][right-1] && s[left] == s[right])
                        status[left][right] = status[left+1][right-1] + 2;
                }
            }
        }
        left = 0;
        int max_len = 0;
        for(int i = 0; i < lens; i++)
            for(int j = i; j < lens; j++){
                if(status[i][j] > max_len){
                    max_len = status[i][j];
                    left = i;
                }
            }
        return s.substr(left, max_len);
    }
};
```

# Expand Around Center
思想如名所示，比较简单，这里注意循环次数是2n-1，因为每个间隔也要进行expand。



```C++
class Solution {
public:
    string longestPalindrome(string s) {
        int lens = s.length();
        if(lens == 0)
            return "";
        int max_len = 0;
        int final_left = 0;
        for(int i = 0; i < (2*lens - 1); i++){
            if(i % 2 == 0){
                int mid = i / 2;
                int temp_len = 1;
                int left = mid - 1;
                int right = mid + 1;
                while(left >= 0 && right < lens && s[left] == s[right]){
                    temp_len += 2;
                    left -= 1;
                    right += 1;
                }
                if(temp_len > max_len){
                    final_left = left + 1;
                    max_len = temp_len;
                }
            } else {
                int mid = i / 2;
                int temp_len = 0;
                int left = mid;
                int right = mid + 1;
                while(left >= 0 && right < lens && s[left] == s[right]){
                    temp_len += 2;
                    left -= 1;
                    right += 1;
                }
                if(temp_len > max_len){
                    final_left = left + 1;
                    max_len = temp_len;
                }
            }
        }
        return s.substr(final_left, max_len);
    }
};
```

