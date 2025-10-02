#🧮 Number-Based Problems
# 1)Reverse a number
```
def reverse_number(num):
    new_num = 0
    while num:
        new_num = new_num*10 + (num%10)
        num = num // 10
    return new_num
```

# 2)Reverse a number by converting to string
```
def reverse_number2(num):
    reverse_num = str(num)[::-1]
    return int(reverse_num)
```

# 3)Count number of digits in a given number
```
def count_numbers(num):
    new_num = 0
    while num:
        num = num // 10
        new_num += 1
    return new_num
```

# 4)Check if a number is palindrome using while loop (best case)
```
def palindrome(num):
    rnum = 0
    while num:
        rnum = rnum*10 + (num % 10)
        num = num // 10
    return num == rnum
```

# 5)Check if a number is palindrome by converting to string and using slicing
```
def palindrome2(number):
    str_num = str(number)
    return str_num == str_num[::-1]
```

# 6)Check if a number is prime using flag and n // 2 + 1
```
def prime(num):
    if num <= 0:
        return False

    flag = False

    for i in range(2, (num // 2) + 1):
        if num % i == 0:
            flag = True
            break

    return not flag
```

# 7)Check if a number is prime using for-else loop (Best)
```
def prime2(num):
    if num <= 1:
        return False

    for i in range(2, (num // 2) + 1):
        if num % i == 0:
            return False
    else:
        return True
```

# 8)Find all prime numbers in a range using for-else (Best)
```
def prime_range(start, end):
    for num in range(start, end + 1):
        if num <= 1:
            continue
        for i in range(2, (num // 2) + 1):
            if num % i == 0:
                break
        else:
            print(num, end=' ')
```

# 9)Find all prime numbers in a range using flag method
```
def prime_range2(start, end):
    for num in range(start, end+1):
        if num <= 1:
            continue

        flag = False

        for i in range(2, (num // 2) + 1 ):
            if num % i == 0:
                flag = True
                break

        if flag == False:
            print(num, end=' ')
```

# 10)Find sum of digits of a number
```
def sum_of_digits(num):
    total = 0
    while num:
        total += num % 10
        num = num // 10
    return total
```

# 11)Find factorial of a number using recursion
```
def factorial(num):
    if num == 0 or num == 1:
        return 1
    else:
        return num * factorial(num - 1)
```

# 12)Find factorial of a number using while loop
```
def factorial2(num):
    result = 1
    while num:
        result = result * num
        num -= 1
    return num
```

# 13)Find factorial of a number using while loop
```
def factorial3(num):
    result = 1
    for i in range(1, num+1):
        result = result *  i
```

# 14)Check if a number is an Armstrong number
```
def armstrong(num):
    orignal = num
    result = 0
    digits = len(str(num))
    while num:
        result += (num%10)**digits
        num = num//10
    return orignal == result
```

# 15)Find all Armstrong numbers in a given range
```
def armstrong_range(start, end):
    for i in range(start, end):
        orignal = i
        result = 0
        digits = len(str(i))
        while i:
            result += (i%10)**digits
            i = i//10
        if orignal == result:
            print(orignal)
```

# 16)Find sum of factorial of digits of a number like 145 = 1! + 4! + 5!
```
def factorial_sum(num):
    total = 0
    temp = num
    while temp:
        total += factorial(temp%10)
        temp = temp//10
    return num == total
```

# 17)Find largest number in a list using for loop
```
def largest(nums):
    largest = 0
    for i in nums:
        if i > largest:
            largest = i
    return largest
```

# 18)Find second largest number in a list using for loop
```
def second_largest(nums):
    if len(nums) < 2:
        return None

    second = largest = float('-inf')

    for i in nums:
        if i > largest:
            second = largest
            largest = i
        elif largest > i > second:
            second = i

    return second
```

# 19)Find second largest number using reverse and sort
```
def second_largest2(nums):
    if len(nums) < 2:
        return None

    nums.sort(reverse=True)
    largest = nums[0]
    for num in nums:
        if num < largest:
            return num
    return None
```

# 20)Find second largest number using set and max()
```
def second_largest(nums):
    unique = set(nums)
    if len(unique) < 2:
        return None
    unique = unique.remove(max(unique))
    return max(unique)
```

# 21)Find missing number in range (1 to n)
```
def find_missing_number(arr, n):
    expected_sum = n(n+1)//2
    actual_sum = sum(arr)
    return expected_sum - actual_sum
```


# 22)Implement a basic calculator (support +, -, *, /)
```
def calculator(a, b, operator):
    if operator == '+':
        return a + b
    elif operator == '-':
        return a - b
    elif operator == '*':
        return a * b
    elif operator == '/':
        if b == 0:
            return "Error: Division by zero"
        return a / b
    else:
        return "Invalid operator"
```

#🔤 String Manipulation
# 23)Reverse a string using slicing
```
def reverse(str):
    str = str[::-1]
    return str
```

# 24)Reverse a string using for loop
```
def reverse2(str):
    reversed_s = ""
    for char in str:
        reversed_s = char + reversed_s
    return reversed_s
```

# 25)Reverse a string using for loop
```
def reverse2(str):
    reversed_s = ''.join(reversed(str))
    return reversed_s
```

# 26)Reverse each word of a string
```
def reverse_words(str):
    words = list(str.split())
    for i in range(0, len(words)):
        words[i] = words[i][::-1]
    return ' '.join(words)
```

# 27)Check if a string is palindrome using slicing
```
def palindrome(str):
    reversed_str = str[::-1]
    return str == reversed_str
```

# 28)Check if a string is palindrome using indexing or for loop
```
def palindrome2(str):
    for i in range(0, len(str)//2):
        if str[i] != str[len(str)-1-i]:
            return False
    return True
```

# 29)Check if a string is palindrome using reversed and join
```
def palindrome3(s):
    reversed_s = ''.join(reversed(s))
    return s == reversed_s
```

# 30)Check if a string is palindrome using while loop
```
def palindrome4(s):
    n = len(s)
    first = 0
    last = n-1
    while(first<last):
        if s[first] == s[last]:
            first += 1
            last -= 1
        else:
            return False
    return True
```

# 31)Count number of words in a string using in built functions
```
def count_words(s):
    words = s.split()
    return len(words)
```

# 32)Count number of words in a string using for loop
```
def count_words2(s):
    in_word = False
    count = 0
    for i in s:
        if i != ' ':
            if in_word == False:
                count += 1
                in_word = True
        else:
            in_word = False
    return count
```

# 33)Count vowels and consonants in a string
```
def count_vowels_consonants(s):
    vowels = 'aeiou'
    vowels_count = 0
    consonant_count = 0
    for i in s:
        if i in vowels:
            vowels_count += 1
        else:
            consonant_count += 1

    return vowels_count, consonant_count
```

# 34)Find duplicate characters in a string
```
def duplicate_characters(s):
    singles = []
    duplicates = []

    for i in s:
        if i in singles:
            if i not in duplicates:
                duplicates.append(i)
        else:
            singles.append(i)
    return duplicates
```

# 37)Print each letter twice from a given string
```
def twice_letter(s):
    new_s = ''
    for i in s:
        new_s += i*2
    return new_s
```

# 38)Convert Subbu123raj to two outputs: Subburaj and 123
```
def manipulate(s):
    alpha = ''
    num = ''
    for i in s:
        if i.isalpha():
            alpha += i
        else:
            num += i
    return alpha, int(num)
```

# 39)Convert 32400121200 to 32412120000
```
def zero_to_end(s):
    new_s = ''
    zeros = ''
    for i in s:
        if i == '0':
            zeros += i
        else:
            new_s += i
    new_s += zeros
    return new_s
```

# 40)Convert 32400121200 to 00003241212
```
def zero_to_front(s):
    new_s = ''
    zeros = ''
    for i in s:
        if i == '0':
            zeros += i
        else:
            new_s += i
    new_s = zeros + new_s
    return new_s
```

# 42)Convert "aBACbcEDed" to two outputs: "abcde" and "ABCDE"
```
def case_seprate(s):
    lower = ''
    upper = ''
    for i in s:
        if i.isupper():
            upper += i
        else:
            lower += i
    return lower, upper
```

# 45)Remove all non-alphabetic characters from a string
```
def only_alpha(s):
    new_s = ''
    for i in s:
        if i.isalpha():
            new_s += i
    return new_s
```

# 46)Check if two strings are anagrams
```
def anagrams(s1,s2):
    s1 = sorted(s1)
    s2 = sorted(s2)
    return s1 == s2

def anagrams_manual(s1, s2):
    if len(s1) != len(s2):
        return False

    freq1 = {}
    freq2 = {}

    for char in s1:
        freq1[char] = freq1.get(char, 0) + 1

    for char in s2:
        freq2[char] = freq2.get(char, 0) + 1

    return freq1 == freq2
```

# 47)Check if two strings are rotations of each other
```
def rotation_check(a, b):
    a = a*2
    return b in a
```

# 48)Group strings with same characters (group anagrams)
```
from collections import defaultdict

def group_strings_by_chars(words):
    groups = defaultdict(list)
    for word in words:
        key = ''.join(sorted(word))
        groups[key].append(word)
    return list(groups.values())
```

# 49)Convert string to int without using int()
```
def covert_to_int(s):
    num = 0
    is_negative = False
    if s[0] == '-':
        is_negative = True
        s = s[1:]

    for char in s:
        digit = ord(char) - ord('0')
        num = (num * 10) + digit

    return -num if is_negative else num
```

# 50)Implement custom split() or join() functions
```
def split_now(s, delimiter=' '):
    result = []
    word = ''
    for i in s:
        if i == delimiter:
            if word:
                result.append(word)
                word = ''
        else:
            word += i

    if word:
        result.append(word)

    return result

def join_now(arr, delimiter=' '):
    s = ''
    for i in range(len(arr)):
        s += arr[i]
        if i != len(arr) - 1:
            s += delimiter
    return s
```

# 51)Find first non-repeating character in a string
```
def non_repeating_character(s):
    for i in s:
        count = 0
        for j in s:
            if j == i:
                count +=1
        if count == 1:
            return i
    return None
```

#🔁 Loop, Logic, and Recursion
# 52)Generate Fibonacci series using while loop
```
def fibonacci(n):
    series = [0, 1]
    count = 2
    i = 0
    while count <= n:
        series.append(series[i] + series[i+1])
        i +=1
        count +=1
    return series
```

# 53)Generate Fibonacci series using for loop
```
def fibonacci2(n):
    series = [0, 1]
    for i in range(2, n+1):
        series.append(series[i-1] + series[i-2])
    return series
```

# 54)Generate Fibonacci series using recursion (best case)
```
def fibonacci3(n):
    if n == 2:
        return [0, 1]
    series=[]
    series.extend(fibonacci3(n-1))
    series.append(series[-1] + series[-2])
    return series
```

# 55)Generate Fibonacci series using generator
```
def fibonacci4(n):
    a = 0
    b = 1
    for i in range(n):
        yield a
        a, b = b, a + b
```

# 56)Generate Fibonacci series without using third variable
```
def fibonacci_no_temp(n):
    a, b = 0, 1
    for _ in range(n):
        print(a, end=' ')
        a, b = b, a + b
```

# 57)Compress string like aabbbcciiiie to a2b3c2i4e1 using for loop (best approach)
```
def string_compress(s):
    ans = ''
    count = 1
    for i in range(1, len(s)):
        if s[i] == s[i-1]:
            count += 1
        else:
            ans += s[i-1] + str(count)
            count = 1
    ans += s[-1] + str(count)
    return ans
```

# 58)Compress string like aabbbcciiiie to a2b3c2i4e1 using while loop
```
def string_compress2(s):
    ans = ''
    count = 1
    i = 1
    while i < len(s):
        if s[i] == s[i-1]:
            count +=1
        else:
            ans += s[i-1] + str(count)
    ans += s[-1] + str(count)
    return ans
```

# 59)Find the pair with sum equal to a given number in a list
```
def pair_finder(arr, target):
    seen = set()
    result = []

    for num in arr:
        diff = target - num
        if diff in seen:
            result.append((diff, num))
        seen.add(num)

    return result
```


# 60)Flatten a nested list
```
def flatten(lst):
    result = []
    for item in lst:
        if isinstance(item, list):
            result.extend(flatten(item))  # recursive call
        else:
            result.append(item)
    return result
```

# 61)Rotate list or string by k positions
```
def rotate_list(lst, k, direction='left'):
    k = k % len(lst) 
    if direction == 'left':
        return lst[k:] + lst[:k]
    else:
        return lst[-k:] + lst[:-k]
```

# 62)Check if brackets/parentheses are balanced


#📊 Data Structures: Lists, Sets, Dictionaries
# 63)Sort a list without using sort() or sorted()
# 64)Sort a dictionary

# 65)Count all characters in a string using dictionary
```
def character_count(s):
    result = {}
    for i in s:
        if i in result.keys():
            result[i] += 1
        else:
            result[i] = 1
        return result
```

# 66)Count least repeating character using dictionary (best)
```
def least_repeating_char(s):
    freq = {}
    for char in s:
        freq[char] = freq.get(char, 0) + 1

    min_freq = min(freq.values())

    for char in s:
        if freq[char] == min_freq:
            return char
```

# 67)Count least repeating character using Counter
```
def least_repeating_char(s):
    from collections import Counter
    freq = Counter(s)
    min_freq = min(freq.values())

    for char in s:
        if freq[char] == min_freq:
            return char
```

# 68)Count a particular element using .count()
```
def count_with_builtin(lst, target):
    return lst.count(target)
```

# 69)Count a particular element without using .count() (use dict) (best)
```
def character_count(s, k):
    result = {}
    for i in s:
        if i in result.keys():
            result[i] += 1
        else:
            result[i] = 1
        return result[k]
```

# 70)Find common elements between two arrays/lists
```
def common_elements(list1, list2):
    return list(set(list1) & set(list2))
```

# 71)Find the first and last element of an List
```
def first_and_last(lst):
    if not lst:
        return None, None
    return lst[0], lst[-1]
```

# 72)Use list comprehension to filter or transform data
# 74)Use map(), filter(), reduce() with lambda


#⚠️ Exceptions and Edge Cases
# 76)Raise a custom exception using code
# 77)Check if a number is a factorial Armstrong number


#🧪 Bonus Practice Challenges
# 78)Implement FizzBuzz using for loop (best approach)
# 79)Implement FizzBuzz using dictionary
# 80)Group characters into lowercase and uppercase separately

# 81)Advanced: Group anagrams or isomorphic strings
