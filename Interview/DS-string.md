# String

## Methods

### Sliding Windows

> https://medium.com/leetcode-patterns/leetcode-pattern-2-sliding-windows-for-strings-e19af105316b

#### Fixed Window Sizes

#### Vary Window Size

## Questions Classify

- ## Noun

  - Anagrams: hash table
  - palindrome(回文): sliding windows
  - alphanumeric: alphabet + numeric
  - Substring:

## Attention

- 

## Leetcode

### Anagrams

#### 49. Group Anagrams

```python
class Solution(object):
    def groupAnagrams(self, strs):
        """
        :type strs: List[str]
        :rtype: List[List[str]]
        """
        strs_dict = {}
        for string in strs:
            key = self.calculateKey(string)
            if key not in strs_dict:
                strs_dict[key] = []
            strs_dict[key].append(string)
        return strs_dict.values()
    
    def calculateKey(self, string):
        key = [0] * 26
        for char in string:
            key[ord(char)-97] += 1
        return tuple(key)
```

#### 242. Valid Anagram

```python
class Solution(object):
    def isAnagram(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        if len(s) != len(t): return False
        s_dict = {}
        t_dict = {}
        for schar, tchar, in zip(s,t):
            if schar in s_dict:
                s_dict[schar] += 1
            else:
                s_dict[schar] = 1
            
            if tchar in t_dict:
                t_dict[tchar] += 1
            else:
                t_dict[tchar] = 1
        
        for skey, svalue in s_dict.items():
            if skey not in t_dict: return False
            elif t_dict[skey] != svalue: return False
        
        return True
```

### Palindrome

#### 125. Valid Palindrome

Tag: Two pointer (front and back)

```python
class Solution(object):
    def isPalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        first = 0
        last = len(s)-1
        while first < last:     # could handle len(s) < 2
            if not s[first].isalnum():
                first += 1
                continue
            if not s[last].isalnum():
                last -= 1
                continue
            if s[first].lower() != s[last].lower():
                return False
            else:
                first += 1
                last -= 1
        return True
```

### Substrings

#### 5. Longest Palindromic Substring

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        def validPalindromic(s: str):
            left = 0
            right = len(s)-1
            while left<right:
                if s[left] != s[right]: return -1
                left += 1
                right -= 1
            return len(s)

        if not s: return s
        ans = s[0]
        for left in range(len(s)):
            right = len(s)-1
            while right+1-left > len(ans):
                # print(s[left:right+1])
                if s[left] != s[right]:
                    right -= 1
                else:
                    validLen = validPalindromic(s[left:right+1])
                    if validLen > 0:
                        if validLen: ans = s[left:right+1]
                        break
                    else:
                        right -= 1
        return ans
```

#### 3. Longest Substring Without Repeating Characters

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        if len(s) == 0: return 0
        ans = 1
        for left in range(len(s)-1):
            right = left+1
            uniq = {}
            uniq[s[left]] = left 
            while right < len(s):
                # print(s[left:right+1])
                if s[right] in uniq:
                    if right-left > ans: ans = right-left
                    break
                else:
                    uniq[s[right]] = right
                    right += 1
            if right-left > ans: ans = right-left
        return ans
```

#### 28. Implement strStr()

```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        if not needle: return 0
        if not haystack: return -1

        size = len(needle)
        for i in range(len(haystack)-size+1):
            # print(i)
            if haystack[i:i+size] == needle:
                return i
        return -1
```

### Prefix

#### 14. Longest Common Prefix

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        if not strs: return ""
        prefix = strs[0]
        for string in strs[1:]:
            i = 0
            while i<len(prefix) and i<len(string):
                if prefix[i] != string[i]: break
                i += 1
            prefix = prefix[:i]
        return prefix
```

### Reverse

#### 344. Reverse String

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        if len(s)>1:
            first = 0
            last = len(s)-1
            while first < last:
                # print(first, last)
                s[first], s[last] = s[last], s[first]
                first += 1
                last -= 1
```

#### 151. Reverse Words in a String

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        slist = s.split()
        if len(slist) < 2: return ' '.join(slist)

        first = 0
        last = len(slist)-1
        while first<last:
            slist[first], slist[last] = slist[last], slist[first]
            first += 1
            last -= 1
        return ' '.join(slist)
```

### idk

#### 20. Valid Parentheses

```python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        if not s: return True
        for para in s:
            if para == '(':
                stack.append(para)
            elif para == '{':
                stack.append(para)
            elif para == '[':
                stack.append(para)
            else:
                if not stack: return False
                elif para == ')':
                    if stack.pop() != '(': return False
                elif para == '}':
                    if stack.pop() != '{': return False
                elif para == ']':
                    if stack.pop() != '[': return False
        if len(stack) != 0: return False
        return True
```

#### 387. First Unique Character in a String

```python
class Solution:
    def firstUniqChar(self, s: str) -> int:
        if not s: return -1
        uniq = {}
        nonuniq = {}
        for index, char in enumerate(s):
            if char in uniq:
                uniq.pop(char)
                nonuniq[char] = index
            elif char in nonuniq: continue
            else: uniq[char] = index
        if not uniq: return -1
        return min(uniq.values())
```

#### 937. Reorder Log Files

```python
class Solution:
    def reorderLogFiles(self, logs: List[str]) -> List[str]:
        digitLogs = []
        letterLogs = []
        for log in logs:
            if log.split(" ")[1].isnumeric(): digitLogs.append(log)
            else:
                letterLogs.append(' '.join(log.split(' ')[1:] + [log.split(' ')[0]]))
            letterLogs.sort()
        return [' '.join([log.split(' ')[-1]]+log.split(' ')[:-1]) for log in letterLogs]+digitLogs
```

#### 38. Count and Say

```python
class Solution:
    def countAndSay(self, n: int) -> str:
        if n < 1: return ""
        ans = "1"
        while n>1:
            n -= 1
            new_ans = ""
            while ans:
                count = 1
                current = ans[0]
                while count<len(ans) and ans[count] == current:
                    count += 1
                ans = ans[count:]
                new_ans += str(count)+current
            ans = new_ans
        return ans
```

#### 165. Compare Version Numbers

```python
class Solution:
    def compareVersion(self, version1: str, version2: str) -> int:
        version1list = version1.split('.')
        version2list = version2.split('.')
        
        idx = 0
        while idx < len(version1list) or idx < len(version2list):
            if idx >= len(version1list):
                if int(version2list[idx]) == 0:
                    idx += 1
                    continue
                else: return -1
            if idx >= len(version2list):
                if int(version1list[idx]) == 0:
                    idx += 1
                    continue
                else: return 1
            if int(version1list[idx]) > int(version2list[idx]): return 1
            if int(version1list[idx]) < int(version2list[idx]): return -1
            idx += 1
        return 0
```

#### 6. ZigZag Conversion

```python
from collections import defaultdict
class Solution:
    def convert(self, s: str, numRows: int) -> str:
        if numRows<2: return s 
        matrix = defaultdict(list)
        row = 0
        col = 0
        while s:
            # print(row, col, s[0])
            matrix[row].append(s[0])
            s = s[1:]
            if col%(numRows-1) == 0:
                if row < numRows-1: row += 1
                else:
                    row = numRows-2
                    col += 1
            else:
                col += 1
                if col%(numRows-1) == 0: row = 0
                else: row = numRows-col%(numRows-1)-1
        # print(matrix)

        ans = ""
        for i in range(numRows):
            ans += "".join(matrix[i])
        return ans
```

