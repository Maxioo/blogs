---
layout: article
title: 2. Add Two Numbers
key: 100005
category: LeetCode
tags: LeetCode
date: 2019-02-18 22:13:00 +08:00
---

Add Two Numbers

Medium题，没什么好说的，类似MergeSort的Merge部分
这里注意一点，最后相加溢出的话要新建立一个节点。

<!--more-->

# Brute Force

```C++
        ListNode* list = new ListNode(0);
        ListNode* ori = list;
        int ad = 0;
        list->val = (l1->val + l2->val)%10;
        ad = (l1->val + l2->val + ad)/10;
        l1 = l1->next;
        l2 = l2->next;
        while(l1 != NULL && l2 != NULL){
            ListNode* n = new ListNode((l1->val + l2->val +ad)%10);
            ad = (l1->val + l2->val + ad)/10;
            list->next = n;
            list = n;
            l1 = l1->next;
            l2 = l2->next;
        }
        while (l1 != NULL){
            ListNode* n = new ListNode((l1->val + ad)%10);
            ad = (l1->val + ad)/10;
            list->next = n;
            list = n;
            l1 = l1->next;
        } 
        while (l2 != NULL){
            ListNode* n = new ListNode((l2->val +ad)%10);
            ad = (l2->val + ad)/10;
            list->next = n;
            list = n;
            l2 = l2->next;
        }
        if (ad != 0){
            list->next = new ListNode(ad);
        }
        return ori;
```

