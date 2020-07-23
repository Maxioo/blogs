---
layout: article
title: 4. Median of Two Sorted Arrays
key: 100010
category: LeetCode
tags: LeetCode
date: 2019-11-23 10:35:00 +08:00
---

Median of Two Sorted Arrays

第一个Hard题，初看题目很简单，给两个增序列表找中值，最简单的办法是类似归并排序最后合并阶段
复杂度:
$$
O(min(m,n))
$$

但是难点在于如何做到
$$
O(log(min(m, n)))
$$
粗看要做到对数复杂度，那么得上二分思想，这里我想了一会儿，就去看Solution了。

思路：

1. 加限制条件，将两个序列的二分过程联系起来。
2. 这个思想来自于一个序列的中值会把序列分成近似相等的两部分，那么在两个子序列中分别抽取一部分元素就可以组成一个新的序列，而且这个序列还是有序的。
3. 那么在这序列的交界部分就是中值产生的位置。

<!--more-->

# Brute Force

归并寻找，代码比较简单就不写了。

# Median Link

Tips：

	1. 注意边界条件。
 	2. 有一些Math intuition。
 	3. 提交后的速度好像并不快，可能是样本不大的缘故，后续待优化。

```C++
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int m = nums1.size(), n = nums2.size();
        if (m == 0 && n != 0 && n%2 != 0)
            return nums2[n/2];
        else if (m == 0 && n != 0 && n%2 == 0)
            return (nums2[n/2-1] + nums2[n/2])/2.0;
        if (n == 0 && m != 0 && m%2 != 0)
            return nums1[m/2];
        else if (n == 0 && m != 0 && m%2 == 0)
            return (nums1[m/2-1] + nums1[m/2])/2.0;
        if (nums2.size() < nums1.size())
            nums1.swap(nums2);
        m = nums1.size();
        n = nums2.size();
        
        double ans = 0;
        
        int l = 0, r = m;
        int loc_m = int(m/2), loc_n = int( (m + n) / 2 - loc_m);
        while(true){
            if (loc_n == 0 && loc_m == m && nums1[loc_m-1] <= nums2[loc_n]){
                if ((m+n)%2 != 0) 
                    ans = nums2[loc_n];
                else
                    ans = (nums2[loc_n] + nums1[loc_m-1]) / 2.0;
                break;
            }
            else if (loc_n == n && loc_m == 0 && nums1[loc_m] >= nums2[loc_n-1]){
                if ((m+n)%2 != 0) 
                    ans = nums2[loc_n-1];
                else
                    ans = (nums2[loc_n-1] + nums1[loc_m]) / 2.0;
                break;
            }
            else if (loc_m == m && nums1[loc_m-1] <= nums2[loc_n]){
                cout << "Here";
                if ((m+n)%2 != 0) 
                    ans = nums2[loc_n];
                else
                    ans = (nums2[loc_n] + max(nums1[loc_m-1], nums2[loc_n-1])) / 2.0;
                break;
            }
            //else if (loc_n == n && nums2[n-1] <= nums1[loc_m]){
            //    if ((m+n)%2 == 0) 
            //        ans = (nums2[n-1] + nums1[loc_m]) / 2.0;
            //    else
            //        ans = nums2[n-1];
            //    break;
            //}
            else if (loc_m == 0 && nums1[loc_m] >= nums2[loc_n - 1]){
                if ((m+n)%2 == 0) 
                    ans = (min(nums1[loc_m], nums2[loc_n]) + nums2[loc_n-1]) / 2.0;
                else
                    ans = min(nums2[loc_n], nums1[loc_m]);
                break;
            }
            //else if (loc_m == m && nums1[m-1] <= nums2[loc_n]){
            //    if ((m+n)%2 != 0) 
            //        ans = nums2[loc_n];
            //    else
            //        ans = (max(nums1[loc_m-1],nums2[loc_n-1]) + nums2[loc_n]) / 2.0;
            //    break;
            //}
            else if (loc_m >0 && loc_n > 0 && nums1[loc_m-1] <= nums2[loc_n] && nums2[loc_n-1] <= nums1[loc_m]){
                if ((m+n)%2 == 0) 
                    ans = (max(nums2[loc_n - 1], nums1[loc_m - 1]) + min(nums2[loc_n], nums1[loc_m])) / 2.0;
                else
                    ans = min(nums2[loc_n], nums1[loc_m]);
                break;
            }
            else if (nums1[loc_m] < nums2[loc_n - 1]){
                l = loc_m+1;
                loc_m = int((l + r) / 2);
                loc_n = int( (m + n) / 2 - loc_m);
                continue;
            } else if (nums2[loc_n] < nums1[loc_m - 1]){
                r = loc_m-1;
                loc_m = int((l + r) / 2);
                loc_n = int( (m + n) / 2 - loc_m);
                continue;
            }
        }
        return ans;
    }
};
```
