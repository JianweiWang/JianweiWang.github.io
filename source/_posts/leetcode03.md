---
title: leetcode03
date: 2019-05-04 22:30:10
tags:
---
## 	Longest Common Prefix
### [问题描述](https://leetcode.com/problems/longest-common-prefix/)
<!--more-->
### 解答
```
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs.length < 1) {
            return "";
        }

		List<char[]> chars = new ArrayList<>();
		int _minLength = strs[0].length();
		for (String s: strs) {
			chars.add(s.toCharArray());
			if (_minLength > s.length()) {
				_minLength = s.length();
			}
		}

		List<Character> result = new ArrayList<>();
		boolean breaked = false;
		for (int i = 0; i < _minLength; i++) {
			char ch1 = chars.get(0)[i];
			for (int j = 1; j < strs.length; j++) {
				if (chars.get(j)[i] != ch1) {
					breaked = true;
					break;
				}
			}
			if (breaked) {
				break;
			}
			result.add(ch1);
		}

		if (result.size() == 0) {
			return "";
		} else {
			StringBuilder sb = new StringBuilder();
			for (Character character: result) {
				sb.append(character);
			}
			return sb.toString();
		}
	}
}
```

## Valid Parentheses

### [问题描述](https://leetcode.com/problems/valid-parentheses/)
### 解答
```
class Solution {
   public boolean isValid(String s) {
        char[] chars = s.toCharArray();

       if (chars.length == 0 ) {
           return true;
       }

       if (chars.length < 2 || chars.length % 2 != 0) {
           return false;
       }

        char[] stack = new char[chars.length];
        int j = 0;
        stack[0] = chars[0];
        for (int i = 1; i < chars.length; i++) {
            if (j >= 0 && (stack[j] == '('  && chars[i] == ')'
                    || stack[j] == '[' && chars[i] == ']'
                    || stack[j] == '{' && chars[i] == '}') ) {
                j--;
            } else {
                stack[j+1] = chars[i];
                j = j + 1;
            }
        }

        if (j == -1) {
            return true;
        }

        return false;
    }
}
```

$$
\sum
$$
