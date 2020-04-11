---
layout: article
title: 7. Reverse Integer
key: 100015
category: LeetCode
tags: LeetCode
date: 2020-04-11 21:06:00 +08:00
---

Reverse Integer

简单题


# Brute Force

重点为在进行进位之前要对溢出进行判断。

1. $2^{31}-1$ 数值为 2147483647
2. $2^{31}$ 的 尾数为8
3. 要考虑到负数和正数。

```c++
class Solution {
public:
    int reverse(int x) {
        const int INTMAX = 2147483647;
        int rev = 0;
        while(x){
            int left = x % 10;
            x = x / 10;
            if(rev > INTMAX/10 || rev < -INTMAX/10)
                return 0;
            else if (rev == INTMAX/10){
                if(left > 7)
                    return 0;
                else if (left < -8)
                    return 0;
            }
            rev = rev * 10 + left;
        }
        return rev;
    }
};
```