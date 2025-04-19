---
layout: post
title:  "LeetCode 66.Plus One"
categories: [ Array , Math, Meta ]
author: Souren
image: assets/images/leetCode.png
---


---

### **66. Plus One**


You are given a large integer represented as an integer array `digits`, where each `digits[i]` is the $i^{th}$ digit of the integer. The digits are ordered from most significant to least significant in left-to-right order. The large integer does not contain any leading 0's.

Increment the large integer by one and return the resulting array of digits.

**Example 1:**

```
Input: digits = [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
Incrementing by one gives 123 + 1 = 124.
Thus, the result should be [1,2,4].
```

**Example 2:**

```
Input: digits = [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.
Incrementing by one gives 4321 + 1 = 4322.
Thus, the result should be [4,3,2,2].
```

**Example 3:**

```
Input: digits = [9]
Output: [1,0]
Explanation: The array represents the integer 9.
Incrementing by one gives 9 + 1 = 10.
Thus, the result should be [1,0].
```

---
## I have come up with three solution 

### 1. String Conversion Approach
```python
d = ''.join(str(v) for v in digits)
m = [int(i) for i in str(int(d)+1)]
return m
```
**Description**: Converts the digit array to a string, joins it into a number, converts it to an integer, adds one, converts the result back to a string, and then creates a new list of integers.

**Pros**:
- Simple and easy to understand.
- Handles all cases (including large numbers) correctly.

**Cons**:
- Inefficient due to string conversion and memory allocation for a new list.
- Time complexity: O(n) for conversion and creating the new list, where n is the length of the digits array.
- Space complexity: O(n) for the new list and string operations.
- Less "natural" for the problem, as it relies on type conversions rather than directly manipulating the digits.

### 2. Iterative Digit-by-Digit Approach (First While Loop)
```python
n = len(digits) - 1
while n >= 0:
    if digits[n] == 9:
        digits[n] = 0
    else:
        digits[n] += 1
        return digits
    n -= 1
return [1] + digits
```
**Description**: Iterates through the digits from right to left. If a digit is 9, it sets it to 0 and continues. If a digit is not 9, it increments it and returns the result. If all digits are 9, it prepends a 1 to the array.

**Pros**:
- Operates in-place, modifying the input array (except when prepending a 1).
- Time complexity: O(n) in the worst case (e.g., `[9, 9, 9]`), but often faster for cases where early digits are not 9.
- Space complexity: O(1) for most cases, O(n) when a new list is created with `[1] + digits`.
- Intuitive and directly manipulates digits.

**Cons**:
- Slightly less concise than the third approach due to explicit loop and conditionals.
- The `[1] + digits` operation creates a new list, which is less efficient when it occurs.

### 3. Carry-Based Approach
```python
n = len(digits)
carry = 1
for i in range(n - 1, -1, -1):
    digits[i] += carry
    carry = digits[i] // 10
    digits[i] %= 10
    if carry == 0:
        return digits
if carry == 1:
    digits.insert(0, 1)
return digits
```
**Description**: Iterates from right to left, adding a carry (initially 1) to each digit. The carry is updated based on whether the sum exceeds 9, and the digit is set to the remainder (`% 10`). If a carry remains after the loop, a 1 is inserted at the start.

**Pros**:
- In-place modification (except when inserting a 1).
- Time complexity: O(n) in the worst case, but optimized with early exit when `carry == 0`.
- Space complexity: O(1) for most cases, O(n) only when inserting a 1.
- Elegant and mimics the arithmetic process of adding 1.
- Handles all edge cases cleanly.

**Cons**:
- Slightly more complex to understand due to carry logic.
- The `insert(0, 1)` operation is O(n), though it happens only in rare cases (e.g., `[9, 9, 9]`).

### Comparison and Recommendation
| **Aspect**              | **String Conversion** | **Iterative Digit-by-Digit** | **Carry-Based** |
|-------------------------|-----------------------|------------------------------|-----------------|
| **Time Complexity**     | O(n)                 | O(n)                        | O(n)           |
| **Space Complexity**    | O(n)                 | O(1) or O(n)                | O(1) or O(n)   |
| **In-Place**            | No (new list)        | Yes (except for prepend)    | Yes (except for insert) |
| **Clarity**             | High                 | Moderate                    | Moderate       |
| **Efficiency**          | Low                  | High                        | High           |
| **Edge Case Handling**  | Robust               | Robust                      | Robust         |

**Best Approach**: The **Carry-Based Approach** (third approach) is the best overall. It is:
- **Efficient**: Operates in-place for most cases and has clear, arithmetic-based logic.
- **Robust**: Handles all edge cases (e.g., `[9, 9, 9]`, `[1, 2, 3]`) correctly.
- **Concise**: Balances clarity and compactness without relying on type conversions.
- **Scalable**: Mimics how addition works mathematically, making it easier to extend to similar problems.

The **Iterative Digit-by-Digit Approach** is a close second, as it’s also efficient and intuitive but slightly less elegant due to the explicit conditional checks. The **String Conversion Approach** is the least desirable due to its inefficiency and reliance on type conversions, which are unnecessary for this problem.

**Conclusion**: The carry-based approach is the best due to its efficiency, in-place operation, and clear arithmetic logic.

**Souren**

{% include adsense.html %}
