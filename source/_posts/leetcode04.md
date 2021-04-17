---
title: leetcode04
date: 2020-11-14 17:40:15
tags: alogrithm
---
## 两数相加
给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

链接：https://leetcode-cn.com/problems/add-two-numbers

<!--more-->

## 解题思路

1. 两个非负整数相加有可能超过10，因此需要一个变量标记链表中两个节点之和是否超过10；
2. 第二个关键点是如何判断指针是否到了链表尾部，分为2中情况
```
1、2个链表不一样长；
2、2个链表一样长；
其实上面2中情况可以通过一定的手段归结为一种情况，即：对于较短的链表，在其尾部补上值为0的节点即可；
3、我们需要2个指针分表指向当前节点
```

3. 为了减少内存开销，我们可以把计算结果存储到两个链表中的一个。
4. 因为我们前面同步补0的方式把两个链表长度变为一样长，因此需要标志位标记下什么时候2个链表被补齐了；

## 实现
综上，总体算法如下：

```golang
func AddTowNumber(l1 *ListNode, l2 *ListNode) *ListNode {
	h1 := l1
	h2 := l2
	before := h1
	carry := 0
	flag := false
	flag1 := false

	for ; ; {
		if h1.Next == nil {
			h1.Next = &ListNode{0 , nil}
			flag = true
		}

		if h2.Next == nil {
			h2.Next = &ListNode{0, nil}
			flag1 = true
		}

		if h1.Val == 0 && h2.Val == 0 && flag1 && flag{
			break
		}

		sum := h1.Val + h2.Val + carry
		if sum >= 10 {
			carry = 1
			sum -= 10
		} else {
			carry = 0
		}
		h1.Val = sum
		before = h1
		h1 = h1.Next
		h2 = h2.Next
	}

	before.Next = nil
	h1 = before

	if carry > 0 {
		tmp := ListNode{1, nil}
		h1.Next = &tmp
	}

	for ; l1.Next != nil; l1 = l1.Next {
		fmt.Println(l1.Val)
	}

	fmt.Println(l1.Val)

	return l1
}
```
