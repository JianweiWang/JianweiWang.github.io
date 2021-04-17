---
title: leetcode02
date: 2019-05-04 22:21:52
tags: alogrithm
---
## Palindrome Number
### 问题描述
Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.
<!--more-->

#### Example 1:
```
Input: 121
Output: true
```
#### Example 2:

```
Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
```

#### Example 3:
```
Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

### 解答
```
class Solution {
    public boolean isPalindrome(int x) {
        if (x < 0) {
            return false;
        }

        List<Integer> digitals = getNumbers(x);
        int count = digitals.size();
        for (int i = 0; i < count / 2; i++) {
            if (digitals.get(i) != digitals.get(count - 1 - i)) {
                return false;
            }
        }

        return true;
    }

    private List<Integer> getNumbers(int x) {
        List<Integer> digitals = new ArrayList<Integer>();
        long y = (long)x;
        for (;y > 0;) {
            int z = (int) (y % 10);
            digitals.add(z);
            y = y / 10;
        }

        return digitals;
    }
}
```

## 	Roman to Integer
### [问题描述](https://leetcode.com/problems/roman-to-integer/)
### 解答
```
class Solution {
    public int romanToInt(String s) {
		int num = 0;
		char[] chars = s.toCharArray();

		for (int i = 0; i < chars.length; ) {
			char cur = chars[i];

			switch (cur) {
			case 'I':
				if (i == chars.length - 1) {
					num += 1;
					i++;
				} else {
					char next = chars[i + 1];
					if (next == 'V') {
						num += 4;
						i += 2;
					} else if (next == 'X') {
						num += 9;
						i += 2;
					} else {
						num += 1;
						i++;
					}
				}
				break;
			case 'X':
				if (i == chars.length - 1) {
					num += 10;
					i++;
				} else {
					char next = chars[i + 1];
					if (next == 'L') {
						num += 40;
						i += 2;
					} else if (next == 'C') {
						num += 90;
						i += 2;
					} else {
						num += 10;
						i++;
					}
				}
				break;
			case 'C':
				if (i == chars.length - 1) {
					num += 100;
					i++;
				} else {
					char next = chars[i + 1];
					if (next == 'D') {
						num += 400;
						i += 2;
					} else if (next == 'M') {
						num += 900;
						i += 2;
					} else {
						num += 100;
						i++;
					}
				}
				break;

			case 'V':
				num += 5;
				i++;
				break;
			case 'L':
				num += 50;
				i++;
				break;
			case 'D':
				num += 500;
				i++;
				break;
			case 'M':
				num += 1000;
				i++;
			}
		}

		return num;
	}
}
```
