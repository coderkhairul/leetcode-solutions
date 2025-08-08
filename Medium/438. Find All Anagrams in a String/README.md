# 438 — Find All Anagrams in a String

**Problem Link:** [LeetCode #438 - Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/)

## Description
Given two strings `s` and `p`, return an array of **all start indices** of `p`'s anagrams in `s`. An **anagram** is any permutation of the characters in `p`.  
You may return the answer in any order. :contentReference[oaicite:0]{index=0}

### Examples
- **Example 1:**  
Input: s = "cbaebabacd", p = "abc"
Output: [0, 6]
Explanation:
The substring starting at index 0 is "cba", which is an anagram of "abc".
The substring starting at index 6 is "bac", which is an anagram of "abc".

- **Example 2:**  
Input: s = "abab", p = "ab"
Output: [0, 1, 2]
Explanation:
The substrings are "ab", "ba", and "ab"—all anagrams of "ab".


### Approach / Solution Overview
We can solve this efficiently using a **sliding window** with character-frequency counting:
1. Use two frequency counters/maps—one for string `p` (`p_count`) and one for the current window in `s` (`window_count`).
2. Initialize the window on the first `len(p)` characters of `s`.
3. Slide the window over `s`: for each step, increment the count of the new right character, decrement the count of the left (outgoing) character, and remove it if its count drops to zero.
4. Whenever `window_count` matches `p_count`, the current window is an anagram—so record the starting index. :contentReference[oaicite:3]{index=3}

### Complexity Analysis
| Metric             | Value                       |
|--------------------|-----------------------------|
| **Time Complexity** | O(n), where n = length of `s` |
| **Space Complexity** | O(k), where k is the size of the character set (constant, e.g., 26) :contentReference[oaicite:4]{index=4} |

### Python Solution
```python
from collections import Counter
from typing import List

class Solution:
  def findAnagrams(self, s: str, p: str) -> List[int]:
      if len(p) > len(s):
          return []

      p_count = Counter(p)
      window_count = Counter(s[:len(p)])
      result = []

      if window_count == p_count:
          result.append(0)

      for i in range(len(p), len(s)):
          window_count[s[i]] += 1
          window_count[s[i - len(p)]] -= 1
          if window_count[s[i - len(p)]] == 0:
              del window_count[s[i - len(p)]]
          if window_count == p_count:
              result.append(i - len(p) + 1)

      return result
``` :contentReference[oaicite:5]{index=5}

---

Feel free to personalize the README by adding:
- Your **own approach notes** or logic explanation
- Observations on **edge cases** (e.g., empty strings, `p` longer than `s`, no anagrams)
- Comments about any **optimizations or variants** you implemented

Bol—arah-dire assistance lagle chinta na kore bolo!
::contentReference[oaicite:6]{index=6}
