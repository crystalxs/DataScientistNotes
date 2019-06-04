# String

## Noun

- palindrome: 回文
- alphanumeric: alphabet + numeric

## Leetcode

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

## 67. Add Binary

```python
class Solution(object):
    def addBinary(self, a, b):
        """
        :type a: str
        :type b: str
        :rtype: str
        """
        carry = 0
        ap = len(a)-1
        bp = len(b)-1
        binarysum = ""
        while ap >= 0 or bp >= 0 or carry != 0:
            if ap < 0 and bp < 0:
                binarysum = bin(carry)[2:] + binarysum
                return binarysum
            elif ap < 0:
                carry = int(b[bp])+carry
                bp -= 1
            elif bp < 0:
                carry = int(a[ap])+carry
                ap -= 1
            else:
                carry = int(a[ap])+int(b[bp])+carry
                bp -= 1
                ap -= 1
            if carry%2 == 1:
                binarysum = "1" + binarysum
                carry -= 1
            else:
                binarysum = "0" + binarysum
            if carry > 1: carry -= 1
        return binarysum
```

## 125. Valid Palindrome

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

#### 242. Valid Anagram

Tag: string, hash table

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

## 5. Longest Palindromic Substring

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

## 20. Valid Parentheses

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

## 387. First Unique Character in a String

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

## 937. Reorder Log Files

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

## 3. Longest Substring Without Repeating Characters

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

## 8. String to Integer (atoi)

