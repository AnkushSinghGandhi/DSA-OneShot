# 🐍 Python Coding Solutions – Master List

This file contains detailed solutions, explanations, and visual aids for the problems listed in `Readme.md`.

---

## 🧮 Number-Based Problems

### 1. Reverse a number
**Explanation:**  
To reverse a number, we repeatedly extract the last digit using the modulo operator (%) and append it to a new number, shifting the existing digits of the reversed number by one place (multiplying by 10) in each step.

**Visual logic (ASCII):**
```text
Original: 123
Step 1: 123 % 10 = 3, Rev = 0 * 10 + 3 = 3, Num = 123 // 10 = 12
Step 2: 12 % 10 = 2,  Rev = 3 * 10 + 2 = 32, Num = 12 // 10 = 1
Step 3: 1 % 10 = 1,   Rev = 32 * 10 + 1 = 321, Num = 1 // 10 = 0
Result: 321
```

**Solution:**
```python
def reverse_number(n):
    rev = 0
    while n > 0:
        rev = (rev * 10) + (n % 10)
        n //= 10
    return rev
```

---

### 2. Count number of digits in a given number
**Explanation:**  
Digits can be counted by repeatedly dividing the number by 10 until it reaches zero. Each division represents one digit. Alternatively, converting the number to a string and taking the string length is a quick way in Python.

**Solution:**
```python
# Mathematical Approach
def count_digits(n):
    count = 0
    while n > 0:
        n //= 10
        count += 1
    return count

# String Slicing Approach
def count_digits_str(n):
    return len(str(n))
```

---

### 3. Check if a number is palindrome
**Explanation:**  
A number is a palindrome if it reads the same from left to right as from right to left (e.g., 121). We can verify this by reversing the number and checking if the reverse equals the original.

**Solution:**
```python
def is_palindrome(n):
    # Method 1: Slicing
    return str(n) == str(n)[::-1]

    # Method 2: Mathematical (Reversing)
    # val = reverse_number(n)
    # return val == n
```

---

### 4. Check if a number is prime
**Explanation:**  
A prime number is only divisible by 1 and itself. We check for divisibility from 2 up to the square root of the number (or n // 2). If no divisor is found, it's prime.

**Visual (ASCII):**
```text
Checking 7:
7 / 2? No
7 / 3? No
End check (sqrt(7) is ~2.6). Result: PRIME
```

**Solution:**
```python
# Using flag and loop
def is_prime(n):
    if n <= 1: return False
    for i in range(2, int(n**0.5) + 1):
        if n % i == 0:
            return False
    return True
```

---

### 5. Check if a number is an Armstrong number
**Explanation:**  
A number is an Armstrong number (Narcissistic) if the sum of its own digits each raised to the power of the number of digits equals the number itself (e.g., 153 = 1³ + 5³ + 3³).

**Solution:**
```python
def is_armstrong(n):
    s = str(n)
    power = len(s)
    total = sum(int(digit)**power for digit in s)
    return total == n
```

---

### 6. Find all prime numbers in a range
**Explanation:**  
Iterate from the start to the end of the range. For each number, apply the primality test logic.

**Solution:**
```python
def find_primes_in_range(start, end):
    primes = []
    for num in range(start, end + 1):
        if num > 1:
            for i in range(2, int(num**0.5) + 1):
                if (num % i) == 0:
                    break
            else:
                primes.append(num)
    return primes
```

---

### 7. Find factorial of a number
**Explanation:**  
Factorial of n (n!) is the product of all integers from 1 up to n. It can be solved iteratively with a loop or recursively.

**Solution:**
```python
# Iterative
def factorial_loop(n):
    res = 1
    for i in range(2, n + 1):
        res *= i
    return res

# Recursive
def factorial_recv(n):
    if n == 0 or n == 1: return 1
    return n * factorial_recv(n - 1)
```

---

### 8. Find second largest number in a list
**Explanation:**  
The most efficient way is to keep track of the largest and second-largest numbers in a single pass.

**Solution:**
```python
def second_largest(nums):
    first = second = float('-inf')
    for n in nums:
        if n > first:
            second = first
            first = n
        elif n > second and n != first:
            second = n
    return second
```

---

### 9. Find missing number in range 1 to n
**Explanation:**  
Using the formula for the sum of the first n natural numbers: `Sum = n * (n + 1) // 2`. The missing number is the difference between this expected sum and the actual sum.

**Solution:**
```python
def find_missing(nums, n):
    expected_sum = n * (n + 1) // 2
    return expected_sum - sum(nums)
```

---

## 🔤 String Manipulation

### 1. Reverse a string
**Explanation:**  
Strings in Python are immutable, but we can easily reverse them using slicing (`[::-1]`) or by joining a reversed iterator.

**Solution:**
```python
def reverse_string(s):
    # Method 1: Slicing (Fastest/Pythonic)
    return s[::-1]

    # Method 2: Reverse iterator
    # return "".join(reversed(s))
```

---

### 2. Reverse each word in a string
**Explanation:**  
To reverse each word while keeping the word order, we split the string into words, reverse each individual word, and join them back with spaces.

**Example:** `"Hello World"` → `"olleH dlroW"`

**Solution:**
```python
def reverse_each_word(s):
    words = s.split()
    reversed_words = [word[::-1] for word in words]
    return " ".join(reversed_words)
```

---

### 3. Check if a string is palindrome
**Explanation:**  
Similar to numbers, a string is a palindrome if it's equal to its reverse. For real-world cases, we usually ignore case and spaces.

**Solution:**
```python
def is_string_palindrome(s):
    clean_s = "".join(char.lower() for char in s if char.isalnum())
    return clean_s == clean_s[::-1]
```

---

### 4. Count vowels and consonants
**Explanation:**  
Iterate through the string and check if each character belongs to a set of vowels. If it's an alphabet but not a vowel, it's a consonant.

**Solution:**
```python
def count_v_c(s):
    vowels = "aeiouAEIOU"
    v_count = 0
    c_count = 0
    for char in s:
        if char.isalpha():
            if char in vowels:
                v_count += 1
            else:
                c_count += 1
    return v_count, c_count
```

---

---

### 5. Check if two strings are anagrams
**Explanation:**  
Two strings are anagrams if they contain the same characters with the same frequencies. Sorting both strings and comparing them is the easiest way.

**Solution:**
```python
def are_anagrams(s1, s2):
    return sorted(s1) == sorted(s2)
```

---

### 6. Remove all vowels from a string
**Explanation:**  
Create a new string by filtering out characters that are found in the vowel set.

**Solution:**
```python
def remove_vowels(s):
    vowels = "aeiouAEIOU"
    return "".join(c for c in s if c not in vowels)
```

---

### 7. Find max repeated character
**Explanation:**  
Use a dictionary to count frequencies, then find the key with the maximum value.

**Solution:**
```python
def max_repeating(s):
    if not s: return None
    freq = {}
    for c in s:
        freq[c] = freq.get(c, 0) + 1
    return max(freq, key=freq.get)
```

---

## 🔁 Loop, Logic, and Recursion

### 1. Generate Fibonacci series
**Explanation:**  
The Fibonacci series is a sequence where each number is the sum of the two preceding ones, starting from 0 and 1. We use a simple loop and swap variables to generate it.

**Solution:**
```python
def fibonacci(n):
    a, b = 0, 1
    result = []
    for _ in range(n):
        result.append(a)
        a, b = b, a + b
    return result
```

---

### 2. Check if brackets/parentheses are balanced
**Explanation:**  
Use a stack to track opening brackets. For every closing bracket, check if it matches the top of the stack. If at the end the stack is empty, it's balanced.

**Solution:**
```python
def is_balanced(s):
    stack = []
    pairs = {')': '(', '}': '{', ']': '['}
    for char in s:
        if char in pairs.values():
            stack.append(char)
        elif char in pairs:
            if not stack or stack.pop() != pairs[char]:
                return False
    return len(stack) == 0
```

---

## 📊 Data Structures: Lists, Sets, Dictionaries

### 1. Find common elements between two arrays
**Explanation:**  
The most efficient way to find intersection is by converting one or both arrays to sets and using the intersection operator (`&`).

**Solution:**
```python
def find_common(arr1, arr2):
    # Method 1: Sets (Recommended)
    return list(set(arr1) & set(arr2))
```

---

### 2. Count characters using dictionary
**Explanation:**  
Iterate through the string and maintain a count in a dictionary. Keys are characters, values are their frequencies.

**Solution:**
```python
def char_frequency(s):
    freq = {}
    for char in s:
        freq[char] = freq.get(char, 0) + 1
    return freq
```

---

### 3. Sort a list without using sort()
**Explanation:**  
Implementing a simple sorting algorithm like Bubble Sort. Adjacent elements are compared and swapped if they are in the wrong order.

**Solution:**
```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr
```

---

### 4. Sort a dictionary by values
**Explanation:**  
Use the `sorted()` function with a custom `key` that accesses the dictionary items' values (index 1).

**Solution:**
```python
def sort_dict_by_value(d):
    return dict(sorted(d.items(), key=lambda item: item[1]))
```

---

## 🧪 Bonus Practice Challenges

### 1. Implement FizzBuzz
**Explanation:**  
The classic problem: check for divisibility by 3, 5, or both. Order of checking matters (check 15 first).

**Solution:**
```python
def fizz_buzz(n):
    for i in range(1, n + 1):
        if i % 15 == 0:
            print("FizzBuzz")
        elif i % 3 == 0:
            print("Fizz")
        elif i % 5 == 0:
            print("Buzz")
        else:
            print(i)
```
