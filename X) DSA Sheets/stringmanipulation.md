*STRING MANIPULATION* 

# 1. Reverse a String

**Problem:** Reverse the input string.

```python
def reverse_string(s):
    return s[::-1]
```

**Explanation:** Python slicing `[::-1]` reverses the string efficiently.

---

# 2. Check if a String is a Palindrome

**Problem:** Check if the string reads the same forwards and backwards.

```python
def is_palindrome(s):
    return s == s[::-1]
```

---

# 3. Count the Occurrences of a Character

**Problem:** Count how many times a character appears in a string.

```python
def count_char(s, target):
    count = 0
    for ch in s:
        if ch == target:
            count += 1
    return count
```

Or simply:

```python
def count_char(s, target):
    return s.count(target)
```

---

# 4. Remove All Vowels from a String

**Problem:** Remove vowels (a, e, i, o, u) from a string.

```python
def remove_vowels(s):
    vowels = set('aeiouAEIOU')
    return ''.join(ch for ch in s if ch not in vowels)
```

---

# 5. Check if Two Strings are Anagrams

**Problem:** Check if two strings contain the same characters with the same frequency.

```python
def are_anagrams(s1, s2):
    return sorted(s1) == sorted(s2)
```

Or use frequency counts:

```python
from collections import Counter

def are_anagrams(s1, s2):
    return Counter(s1) == Counter(s2)
```

---

# 6. Find the First Non-Repeating Character

**Problem:** Return the first character that doesn’t repeat in the string.

```python
from collections import Counter

def first_non_repeating_char(s):
    counts = Counter(s)
    for ch in s:
        if counts[ch] == 1:
            return ch
    return None  # if no non-repeating char
```

---

# 7. Reverse Words in a Sentence

**Problem:** Given `"Hello world here"`, return `"here world Hello"`.

```python
def reverse_words(sentence):
    words = sentence.split()
    words.reverse()
    return ' '.join(words)
```

Or one-liner:

```python
def reverse_words(sentence):
    return ' '.join(sentence.split()[::-1])
```

---

# 8. Check if String Contains Only Digits

```python
def is_digit_only(s):
    return s.isdigit()
```

---

# 9. Convert String to Integer (without built-in int())

**Problem:** Convert numeric string to integer manually.

```python
def str_to_int(s):
    result = 0
    for ch in s:
        digit = ord(ch) - ord('0')  # convert char to digit
        result = result * 10 + digit
    return result
```

---

# 10. Remove Duplicates from String

**Problem:** Remove duplicate characters, keeping the first occurrence.

```python
def remove_duplicates(s):
    seen = set()
    result = []
    for ch in s:
        if ch not in seen:
            seen.add(ch)
            result.append(ch)
    return ''.join(result)
```

---

# 11. Check if String is a Rotation of Another

**Problem:** Check if `s2` is a rotation of `s1`. For example, `"erbottlewat"` is a rotation of `"waterbottle"`.

```python
def is_rotation(s1, s2):
    if len(s1) != len(s2):
        return False
    return s2 in s1 + s1
```

---

# 12. Count Number of Words in a String

```python
def count_words(s):
    return len(s.split())
```

---

# 13. Find the Longest Common Prefix

**Problem:** Find the longest common prefix among a list of strings.

```python
def longest_common_prefix(strs):
    if not strs:
        return ''
    prefix = strs[0]
    for s in strs[1:]:
        while not s.startswith(prefix):
            prefix = prefix[:-1]
            if not prefix:
                return ''
    return prefix
```

---

# 14. Implement strstr() or find substring

**Problem:** Return the index of the first occurrence of substring `needle` in string `haystack`, or -1 if not found.

```python
def strstr(haystack, needle):
    if needle == "":
        return 0
    for i in range(len(haystack) - len(needle) + 1):
        if haystack[i:i+len(needle)] == needle:
            return i
    return -1
```

---

# 15. Check if String Has All Unique Characters

```python
def all_unique(s):
    return len(set(s)) == len(s)
```

---

# Want me to provide:

* More problems?
* Patterns and tips for string manipulation?
* Explain solutions line by line?
* Practice questions with increasing difficulty?

Just say!
[30/06, 13:00] Ankush Singh: Absolutely! Here are more common **string manipulation interview questions** with solutions. These cover a variety of problem types and complexity:

---

# 16. Check if Two Strings are Isomorphic

**Problem:** Two strings are isomorphic if characters in `s` can be replaced to get `t`, preserving order and uniqueness.

```python
def is_isomorphic(s, t):
    if len(s) != len(t):
        return False
    mapping_s_t = {}
    mapped_t = set()
    for cs, ct in zip(s, t):
        if cs in mapping_s_t:
            if mapping_s_t[cs] != ct:
                return False
        else:
            if ct in mapped_t:
                return False
            mapping_s_t[cs] = ct
            mapped_t.add(ct)
    return True
```

---

# 17. Check if a String is a Valid Palindrome (ignoring spaces, punctuation, case)

```python
import string

def valid_palindrome(s):
    allowed = set(string.ascii_letters + string.digits)
    filtered = [ch.lower() for ch in s if ch in allowed]
    return filtered == filtered[::-1]
```

---

# 18. Longest Substring Without Repeating Characters

**Problem:** Find length of longest substring with unique characters.

```python
def length_of_longest_substring(s):
    seen = {}
    left = 0
    max_len = 0
    for right, ch in enumerate(s):
        if ch in seen and seen[ch] >= left:
            left = seen[ch] + 1
        seen[ch] = right
        max_len = max(max_len, right - left + 1)
    return max_len
```

---

# 19. Compress String (Basic Run-Length Encoding)

**Problem:** Convert `"aaabbc"` to `"a3b2c1"`.

```python
def compress_string(s):
    if not s:
        return ""
    result = []
    count = 1
    for i in range(1, len(s)):
        if s[i] == s[i-1]:
            count += 1
        else:
            result.append(s[i-1] + str(count))
            count = 1
    result.append(s[-1] + str(count))
    return ''.join(result)
```

---

# 20. Check if One String is a Subsequence of Another

**Problem:** Check if `s` is a subsequence of `t`.

```python
def is_subsequence(s, t):
    i = 0
    for ch in t:
        if i < len(s) and s[i] == ch:
            i += 1
    return i == len(s)
```

---

# 21. Count Palindromic Substrings

**Problem:** Count all substrings of `s` that are palindromes.

```python
def count_palindromic_substrings(s):
    count = 0

    def expand(left, right):
        nonlocal count
        while left >= 0 and right < len(s) and s[left] == s[right]:
            count += 1
            left -= 1
            right += 1

    for i in range(len(s)):
        expand(i, i)      # odd length palindromes
        expand(i, i + 1)  # even length palindromes

    return count
```

---

# 22. Convert String to Title Case

```python
def title_case(s):
    return ' '.join(word.capitalize() for word in s.split())
```

---

# 23. Find All Permutations of a String (without duplicates)

```python
def permutations(s):
    result = []
    s = sorted(s)

    def backtrack(path, used):
        if len(path) == len(s):
            result.append(''.join(path))
            return
        for i in range(len(s)):
            if used[i]:
                continue
            if i > 0 and s[i] == s[i-1] and not used[i-1]:
                continue
            used[i] = True
            path.append(s[i])
            backtrack(path, used)
            path.pop()
            used[i] = False

    backtrack([], [False]*len(s))
    return result
```

---

# 24. Find the Longest Palindromic Substring

```python
def longest_palindrome(s):
    start = 0
    max_len = 1

    def expand(left, right):
        while left >= 0 and right < len(s) and s[left] == s[right]:
            left -= 1
            right += 1
        return left + 1, right - 1

    for i in range(len(s)):
        l1, r1 = expand(i, i)
        l2, r2 = expand(i, i + 1)

        if r1 - l1 + 1 > max_len:
            start = l1
            max_len = r1 - l1 + 1
        if r2 - l2 + 1 > max_len:
            start = l2
            max_len = r2 - l2 + 1

    return s[start:start + max_len]
```

---

# 25. Implement atoi (string to integer with sign and error checking)

```python
def atoi(s):
    s = s.strip()
    if not s:
        return 0
    sign = 1
    i = 0
    if s[0] == '-':
        sign = -1
        i += 1
    elif s[0] == '+':
        i += 1

    num = 0
    while i < len(s) and s[i].isdigit():
        num = num * 10 + (ord(s[i]) - ord('0'))
        i += 1

    return sign * num
```

---

# 26. Check if a String Contains Only Unique Characters (without extra data structures)

```python
def unique_chars_no_ds(s):
    for i in range(len(s)):
        for j in range(i+1, len(s)):
            if s[i] == s[j]:
                return False
    return True
```

---

# 27. Find All Anagrams of a String Within Another String

**Problem:** Find all start indices of `p`’s anagrams in `s`.

```python
from collections import Counter

def find_anagrams(s, p):
    p_count = Counter(p)
    s_count = Counter()
    result = []
    left = 0
    for right in range(len(s)):
        s_count[s[right]] += 1
        if right - left + 1 > len(p):
            s_count[s[left]] -= 1
            if s_count[s[left]] == 0:
                del s_count[s[left]]
            left += 1
        if s_count == p_count:
            result.append(left)
    return result
```

---

# 28. Check if String is a Valid Number (like "123", "-123.45", "1e10")

*Note: This can be complicated, but here’s a simplified validator.*

```python
import re

def is_number(s):
    pattern = re.compile(r'^[-+]?\d*\.?\d+([eE][-+]?\d+)?$')
    return bool(pattern.match(s.strip()))
```

---

# 29. Decode a String with Encoded Pattern

**Problem:** Given `"3[a2[c]]"`, decode to `"accaccacc"`.

```python
def decode_string(s):
    stack = []
    curr_num = 0
    curr_str = ''
    for ch in s:
        if ch.isdigit():
            curr_num = curr_num * 10 + int(ch)
        elif ch == '[':
            stack.append((curr_str, curr_num))
            curr_str = ''
            curr_num = 0
        elif ch == ']':
            last_str, num = stack.pop()
            curr_str = last_str + curr_str * num
        else:
            curr_str += ch
    return curr_str
```

---

# 30. Group Anagrams Together

```python
from collections import defaultdict

def group_anagrams(strs):
    groups = defaultdict(list)
    for s in strs:
        key = tuple(sorted(s))
        groups[key].append(s)
    return list(groups.values())
```

---

# 31. Implement strstr() Using KMP Algorithm (Efficient substring search)

*This is advanced but very common.*

```python
def compute_lps(pattern):
    lps = [0] * len(pattern)
    length = 0
    i = 1
    while i < len(pattern):
        if pattern[i] == pattern[length]:
            length += 1
            lps[i] = length
            i += 1
        else:
            if length != 0:
                length = lps[length-1]
            else:
                lps[i] = 0
                i += 1
    return lps

def kmp_search(text, pattern):
    if not pattern:
        return 0
    lps = compute_lps(pattern)
    i = j = 0
    while i < len(text):
        if text[i] == pattern[j]:
            i += 1
            j += 1
        if j == len(pattern):
            return i - j
        elif i < len(text) and text[i] != pattern[j]:
            if j != 0:
                j = lps[j-1]
            else:
                i += 1
    return -1
```

---

# 32. Validate IPv4 Address

```python
def valid_ip(ip):
    parts = ip.split('.')
    if len(parts) != 4:
        return False
    for part in parts:
        if not part.isdigit():
            return False
        num = int(part)
        if num < 0 or num > 255 or (part[0] == '0' and len(part) > 1):
            return False
    return True
```

---

# 33. Multiply Strings (Large Numbers)

```python
def multiply_strings(num1, num2):
    if num1 == "0" or num2 == "0":
        return "0"
    res = [0] * (len(num1) + len(num2))
    num1 = num1[::-1]
    num2 = num2[::-1]
    for i in range(len(num1)):
        for j in range(len(num2)):
            res[i+j] += int(num1[i]) * int(num2[j])
            res[i+j+1] += res[i+j] // 10
            res[i+j] %= 10
    while res[-1] == 0:
        res.pop()
    return ''.join(map(str, res[::-1]))
```

---

# 34. Remove Adjacent Duplicates Recursively

```python
def remove_adj_duplicates(s):
    i = 0
    while i < len(s) - 1:
        if s[i] == s[i+1]:
            j = i+1
            while j < len(s) and s[j] == s[i]:
                j += 1
            return remove_adj_duplicates(s[:i] + s[j:])
        else:
            i += 1
    return s
```

---

# 35. Check if Parentheses are Balanced

```python
def is_balanced(s):
    stack = []
    pairs = {')':'(', '}':'{', ']':'['}
    for ch in s:
        if ch in pairs.values():
            stack.append(ch)
        elif ch in pairs:
            if not stack or stack.pop() != pairs[ch]:
                return False
    return not stack
```
