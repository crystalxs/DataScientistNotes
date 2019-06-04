# Math

## 7. Reverse Integer

```python
class Solution:
    def reverse(self, x: int) -> int:
        xStr = str(x)
        negative = False
        if xStr[0] == '-':
            negative = True
            numStr = xStr[1:][::-1]
        else:
            numStr = xStr[::-1]
        ans = 0
        for num in numStr:
            ans = ans*10 + int(num)
        if negative:
            ans = -ans
        if ans > 2**31-1 or ans < -2**31:
            return 0
        else:
            return ans
```

## 9. Palindrome Number

```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        xStr = str(x)
        if xStr == xStr[::-1]: return True
        else: return False
```

## 12. Integer to Roman

### Idea

- use `%` to avoid convert to string then iteration;

```python
class Solution:
    def intToRoman(self, num: int) -> str:
        tens = 0
        ans = ""
        while num>0:
            current = num%10
            temp = ''
            num = num//10
            tens += 1
            if tens == 1:
                if current == 4:
                    ans = 'IV' + ans
                    continue
                elif current == 9:
                    ans = 'IX' + ans
                    continue
                elif current >= 5:
                    temp += 'V'
                    current -= 5
                while current > 0:
                    temp += 'I'
                    current -= 1
            elif tens == 2:
                if current == 4:
                    ans = 'XL'+ans
                    continue
                elif current == 9:
                    ans = 'XC'+ans
                    continue
                elif current >= 5:
                    temp += 'L'
                    current -= 5
                while current > 0:
                    temp += 'X'
                    current -= 1
            elif tens == 3:
                if current == 4:
                    ans = 'CD'+ans
                    continue
                elif current == 9:
                    ans = 'CM'+ans
                    continue
                elif current >= 5:
                    temp += 'D'
                    current -= 5
                while current > 0:
                    temp += 'C'
                    current -= 1
            else:
                while current > 0:
                    temp += 'M'
                    current -= 1
            ans = temp+ans
        return ans
```

## 50. Pow(x, n)

```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        if n<0:
            x=1/x
            n = -n
        if n%2 == 1: ans = x
        else: ans = 1
        if n > 1:
            ans *= self.myPow(x, n//2)**2
        return ans
```

## 43. Multiply Strings

```python
class Solution:
    def multiply(self, num1: str, num2: str) -> str:
        num = 0
        tens2 = 0
        while num2:
            tens1 = 0
            current = int(num2[-1])*(10**tens2)
            num2 = num2[:-1]
            num1copy = num1
            while num1copy:
                num += current*int(num1copy[-1])*(10**tens1)
                # print(num)
                num1copy = num1copy[:-1]
                tens1 += 1
            tens2 += 1
        return str(num)
```

## 204. Count Primes

### Idea

- Only test until the $sqrt(n)+1$;
- Only modified the multiples nums, do not loop all;

```python
class Solution:
    def countPrimes(self, n: int) -> int:
        if n<3: return 0
        prime = [True]*n
        prime[0] = prime[1] = False
        for idx in range(2, int(n**0.5)+1):
            if prime[idx]:
                for i in range(idx*idx, n, idx):
                    prime[i] = False
        return sum(prime)
```



