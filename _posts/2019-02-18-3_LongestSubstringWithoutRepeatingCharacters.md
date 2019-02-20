---
layout: article
title: 3. Longest Substring Without Repeating Characters
key: 100006
category: LeetCode
tags: LeetCode
date: 2019-02-18 22:29:00 +08:00
---

Longest Substring Without Repeating Characters

Middle题，这里我刚开始看成找最长回文串了。。

给定一个字符串，找出不带重复字符的最长字串。

<!--more-->

# Brute Force

两个for循环解决，判断每个字串是不是不带重复的子串。
这里注意，一旦在第二个for循环内遇到的子串是带重复的字串，直接break。

这个方法能过，耗时排名在后2%.

```C++
int lengthOfLongestSubstring(string s) {
        if (s.length() == 0)
            return 0;
        int max = 1;
        for (int i = 0; i != s.length() - 1; i++){
            for (int j = i+1; j != s.length(); j++){
                if (isSub(s.substr(i, j-i+1)) == true){
                    if (j-i+1 > max)
                        max = j-i+1;
                } else
                    break;
            }
        }
        return max;
    }
    bool isSub(const string& s){
        for (int ind = 0; ind != s.length() - 1; ind++){
            if (s.find(s[ind], ind+1) != string::npos)
                return false;
        }
        return true;
```

# Sliding Window

维护一个不带重复字符的窗口，窗口可以是任意大小，每次循环前进一个，使用一个Hash表来记录窗口字符，每迭代一次若发现该字符已经出现，那么将窗口左移动一个位置。

```C++
        set<char> hs;
        int max = 0;
        int i = 0, j = 0, n = s.length();
        while(i < n && j < n){
            if (hs.find(s[j]) != hs.end()){
                if (j-i > max) 
                    max = j-i;
                hs.erase(s[i++]);
            } else {
                hs.insert(s[j++]);
                if(j == n && j-i > max)
                    max = j-i;
            }
        }
        return max;
```

# Sliding Window Optimized

我们发现，使用上述滑动窗口需要O(2n)的时间复杂度，而在遇到重复字符的时候，我们每次只移动一个字符，效率很低。

我们可以使用一个HashTable来保持窗口元素和它们对应的位置，我们只需要一个循环，在每次循环过程中，我们每次遇到存在的元素时，窗口左界直接跳转到上个元素位置的下个位置，并更新窗口最大值。这样我们就能在O(n)的时间复杂度内完成。

```C++
        int table[256];
        for (int k = 0; k != 256; k++)
            table[k] = -1;
        int ans = 0;
        int i = 0, j = 0, n = s.length();
        for (; j != n; j++){
            i = max(i, table[s[j]] + 1);
            ans = max(ans, j-i+1);
            table[s[j]] = j;
        }
        return ans;
```