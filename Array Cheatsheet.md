# Array Cheatsheet

Arrays hold values of the **same type** at **contiguous memory locations**. 

### Difference of Array and List in Python 

- List is built in, and array needs import
- An array is faster than a list in python since all the elements stored in an array are homogeneous (they have the same data type), whereas a list contains heterogeneous elements.
- Python arrays are implemented in C which makes it a lot faster than lists that are built-in in Python itself.
- Array has a fixed sized and cannot resize (need to be copied to a bigger array), whereas list can be resized.

> array in python (https://www.guru99.com/array-data-structure.html)

### Advantages of Using Array

- Store multiple elements of the same type with one single variable name
- Accessing elements is fast as long as you have the index, as opposed to [linked lists]() where you have to traverse from the head.


### Disadvantages

- Addition and removal of elements into/from the middle of an array is slow because the remaining elements need to be shifted to accommodate the new/missing element. An exception to this is if the position to be inserted/removed is at the end of the array.

- In Javascript, array size is fixed, it cannot alter its size after initialization. If an insertion causes the total number of elements to exceed the size, a new array has to be allocated and the existing elements have to be copied over. The act of creating a new array and transferring elements over takes O(n) time.

### Common terms


- Subarray - A range of **contiguous values** within an array.
  - Example: given an array `[2, 3, 6, 1, 5, 4]`, `[3, 6, 1]` is a subarray while `[3, 1, 5]` is not a subarray.
  
- Subsequence - A sequence that can be derived from the given sequence by deleting some or no elements without changing the order of the remaining elements.
  - Example: given an array `[2, 3, 6, 1, 5, 4]`, `[3, 1, 5]` is a subsequence but `[3, 5, 1]` is not a subsequence.

### Time Complexity

| **Operation** | **Big-O**  | **Note**  |
| :------- | :--- | :--- |
| Access | O(1) |        |
| Search | O(n) |        |
| Search (**sorted array**) | O(log(n)) | Binary Search       |
| Insert | O(n) | Insertion would require shifting all the subsequent elements to the right by one and that takes O(n)       |
|Insert(at the end)| O(1) | Special case of insertion where no other element needs to be shifted       |
| Remove | O(n) | Removal would require shifting all the subsequent elements to the left by one and that takes O(n)       |
| Remove (at the end) | O(1) |  Special case of removal where no other element needs to be shifted      |

### Things to look out for during interviews

- Clarify if there are **duplicate values** in the array. Would the presence of duplicate values affect the answer? Does it make the question simpler or harder?
- When using an index to iterate through array elements, be careful not to go out of **bounds**.
- Be mindful about slicing or concatenating arrays in your code. Typically, slicing and concatenating arrays would take O(n) time. Use start and end indices to set the **boundary** of a subarray/range where possible.

### Corner cases

- Empty sequence
- Sequence with 1 or 2 elements
- Sequence with repeated elements
- Duplicated values in the sequence

### Techniques

> Note that because both arrays and strings are sequences (a string is an array of characters), most of the techniques here will apply to string problems.

### - Sliding Window

Master the sliding window technique that applies to many subarray/substring problems. 

In a sliding window, the two pointers usually move in the same direction will never overtake each other. This ensures that each value is only visited at most twice and the time complexity is still O(n).

Examples:
> - [Pattern - Sliding Window]()
> - [Problem : Longest Substring Without Repeating Characters - Medium](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
> - [Problem: Minimum Size Subarray Sum - Medium](https://leetcode.com/problems/minimum-size-subarray-sum/)
> - [Problem: Minimum Window Substring - Hard](https://leetcode.com/problems/minimum-window-substring/)


### - Two Pointers

Two pointers is a more general version of sliding window where the pointers can cross each other and can be on different arrays. 

When you are given two arrays to process, it is common to have one index per array (pointer) to traverse/compare the both of them, incrementing one of the pointers when relevant. 

Examples:
> -  [Pattern - Two Pointers]()

### - Traversing from the right

Sometimes you can traverse the array starting from the right instead of the conventional approach of from the left. 

Examples: 
> - [Problem: Daily Temperatures - Medium](https://leetcode.com/problems/daily-temperatures/)
> - [Problem: Number of Visible People in a Queue -Hard](https://leetcode.com/problems/number-of-visible-people-in-a-queue/)

### - Sorting the array

Is the array sorted or partially sorted? If it is, some form of binary search should be possible. This also usually means that the interviewer is looking for a solution that is faster than O(n).

Can you sort the array? Sometimes sorting the array first may significantly simplify the problem. Obviously this would not work if the order of array elements need to be preserved. 

Examples: 
> - [Pattern : Merge Intervals]()
> - [Problem : Merge Intervals - Medium](https://leetcode.com/problems/merge-intervals/)
> - [Non-overlapping Intervals - Medium](https://leetcode.com/problems/non-overlapping-intervals/)

### - Precomputation

For questions where summation or multiplication of a subarray is involved, pre-computation using hashing or a prefix/suffix sum/product might be useful. 

Examples: 

> - [Problem: Product of Array Except Self - Medium](https://leetcode.com/problems/product-of-array-except-self/)
> - [Problem: Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)
> - [Problems: LeetCode questions tagged "prefix-sum"](https://leetcode.com/tag/prefix-sum/)

### Index has a hash key

If you are given a sequence and the interviewer asks for O(1) space, it might be possible to use the array itself as a hash table. For example, if the array only has values from 1 to N, where N is the length of the array, negate the value at that index (minus one) to indicate presence of that number. 

Examples: 

> - [Problem: First Missing Positive - Hard](https://leetcode.com/problems/first-missing-positive/)
> - [Problem: Daily Temperatures - Medium](https://leetcode.com/problems/daily-temperatures/)

### - Traversing the array more than once

This might be obvious, but traversing the array twice/thrice (as long as fewer than n times) is still O(n). Sometimes traversing the array more than once can help you solve the problem while keeping the time complexity to O(n).

## Essential Questions

> - [Problem: Two Sum - Easy](https://leetcode.com/problems/two-sum/)
> - [Problem: Best Time to Buy and Sell Stock - Easy](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
> - [Problem: Product of Array Except Self - Medium](https://leetcode.com/problems/product-of-array-except-self/)
> - [Problem: Maximum Subarray - Medium](https://leetcode.com/problems/maximum-subarray/)
> - [Problem: Contains Duplicate - Easy](https://leetcode.com/problems/contains-duplicate/)
> - [Problem: Maximum Product Subarray - Medium](https://leetcode.com/problems/maximum-product-subarray/)
> - [Problem: Search in Rotated Sorted Array - Medium](https://leetcode.com/problems/search-in-rotated-sorted-array/)
> - [Problem: 3Sum - Medium](https://leetcode.com/problems/3sum/)
> - [Problem: Container With Most Water - Medium](https://leetcode.com/problems/container-with-most-water/)
> - [Problem: Sliding Window Maximum - Hard](https://leetcode.com/problems/sliding-window-maximum/)




