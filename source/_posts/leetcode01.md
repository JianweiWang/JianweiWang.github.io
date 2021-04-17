---
title: leetcode01
date: 2019-05-04 22:09:11
tags:
- LeetCode
categories:
- 算法
---
## Add two numbers
### 问题描述
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example:
```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```
<!--more-->

### 解答
```
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */

func addTwoNumbers1(x, y, val int) (int, int) {
	v1 := x + y + val - 10
	v2 := 0
	if v1 >= 0 {
		v2 = 1
	} else {
		v1 = x + y + val
	}

	return v1, v2
}

func addTwoNumbers(l1 *ListNode, l2 *ListNode) *ListNode {
	node0 := ListNode{0, nil}
	l4 := &node0
	head := &node0
	v3 := 0
	for ; l1 != nil || l2 != nil; {
		v1, v2 := 0, 0
		if l1 != nil && l2 != nil {
			v1, v2 = addTwoNumbers1(l1.Val, l2.Val, v3)
			v3 = v2
			l4.Val = v1

			l1 = l1.Next
			l2 = l2.Next
			if l1 != nil || l2 != nil {
				l4.Next = &ListNode{0, nil}
				l4 = l4.Next
			}
		} else if l2 == nil {
			v1, v2 = addTwoNumbers1(l1.Val, 0, v3)
			v3 = v2
			l4.Val = v1
			l1 = l1.Next
			if l1 != nil {
				l4.Next = &ListNode{0, nil}
				l4 = l4.Next
			}
		} else if l1 == nil {
			v1, v2 = addTwoNumbers1(0, l2.Val, v3)
			v3 = v2
			l4.Val = v1
			l2 = l2.Next
			if l2 != nil {
				l4.Next = &ListNode{0, nil}
				l4 = l4.Next
			}
		}
	}

	if v3 > 0 {
		l4.Next = &ListNode{v3, nil}
	}

	return head
}
```


## Reverse Integer
### 问题描述
Given a 32-bit signed integer, reverse digits of an integer.

#### Example 1:
```
Input: 123
Output: 321
```

#### Example 2:
```
Input: -123
Output: -321
```

#### Example 3:
```
Input: 120
Output: 21
```

**Note:**
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

### 解答
```
class Solution {
    public int reverse(int x) {
        if (x == Integer.MIN_VALUE) {
            return 0;
        }

        List<Integer> digitals = getNumbers(x);

        long value = 0;

        for (int i = digitals.size() - 1; i >= 0; i--) {
            int a = digitals.get(i);
            value += (a * Math.pow(10, digitals.size() - i - 1));
        }

        if (x < 0) {
            value = value * (-1);
        }

        if (value > Integer.MAX_VALUE || value < Integer.MIN_VALUE) {
            return 0;
        }

        return (int) value;
    }

    private List<Integer> getNumbers(int x) {
        List<Integer> digitals = new ArrayList<Integer>();
        long y = (long)x;
        if (x < 0) {
            y = (long)x * (-1);
        }

        for (;y > 0;) {
            int z = (int) (y % 10);
            digitals.add(z);
            y = y / 10;
        }

        return digitals;
    }
}
```
