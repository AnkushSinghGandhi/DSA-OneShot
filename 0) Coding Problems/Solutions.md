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

## 🔁 Loop, Logic, and Recursion

### 1. Generate Fibonacci series
**Explanation:**  
The Fibonacci series is a sequence where each number is the sum of the two preceding ones, starting from 0 and 1.

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

## 🧪 Bonus Practice Challenges

### 1. Implement FizzBuzz
**Explanation:**  
Print numbers from 1 to n. For multiples of 3, print "Fizz"; for multiples of 5, print "Buzz"; for multiples of both, print "FizzBuzz".

**Solution:**
```python
def fizz_buzz(n):
    for i in range(1, n + 1):
        if i % 3 == 0 and i % 5 == 0:
            print("FizzBuzz")
        elif i % 3 == 0:
            print("Fizz")
        elif i % 5 == 0:
            print("Buzz")
        else:
            print(i)
```
