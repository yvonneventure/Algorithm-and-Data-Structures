# Subsets and Permutation

A huge number of coding interview problems involve dealing with **Permutations and Combinations** of a given set of elements. This pattern describes an efficient **Breadth First Search (BFS)** approach to handle all these problems.


### Problem : [Subsets - Medium](https://leetcode.com/problems/subsets/)

> Given a set with distinct elements, find all of its distinct subsets.


Example 1:
```
Input: [1, 3]
Output: [], [1], [3], [1,3]
```
Example 2:
```
Input: [1, 5, 3]
Output: [], [1], [5], [3], [1,5], [1,3], [5,3], [1,5,3]
```

To generate all subsets of the given set, we can use the Breadth First Search (BFS) approach. We can start with an empty set, iterate through all numbers one-by-one, and add them to existing sets to create new subsets.

Let’s take the example-2 mentioned above to go through each step of our algorithm:

Given set: `[1, 5, 3]`

1. Start with an empty set: `[[]]`
2. Add the first number (1) to all the existing subsets to create new subsets: `[[], [1]]`;
3. Add the second number (5) to all the existing subsets: `[[], [1], [5], [1,5]]`;
4. Add the third number (3) to all the existing subsets: `[[], [1], [5], [1,5], [3], [1,3], [5,3], [1,5,3]]`.


Here is the visual representation of the above steps:

<img width="782" alt="Screen Shot 2022-07-18 at 19 33 17" src="https://user-images.githubusercontent.com/103771536/179634005-146f10fd-b8f1-472e-a872-20b50770e582.png">

Since the input set has distinct elements, the above steps will ensure that we will not have any duplicate subsets.

My code:

```python
def find_subsets(arr):
# add empty list
    subsets=[[]]
    for a in arr: 
    
    n=len(subsets)
        for i in range(n):
            set=list(subsets[i])  # set is updated with elements in subsets array
            set.append(a)
            subsets.append(set)

    return print(subsets)

find_subsets([1, 5, 3])
```

#### Time complexity #
Since, in each step, the number of subsets doubles as we add each element to all the existing subsets, the time complexity of the above algorithm is O(2^N), where ‘N’ is the total number of elements in the input set. This also means that, in the end, we will have a total of O(2^N)subsets.

#### Space complexity #
All the additional space used by our algorithm is for the output list. Since we will have a total of O(2^N) subsets, the space complexity of our algorithm is also O(2^N).

### Problem: Subsets With Duplicates

> Given a set of numbers that might contain duplicates, find all of its distinct subsets.

Example 1:
```
Input: [1, 3, 3]
Output: [], [1], [3], [1,3], [3,3], [1,3,3]
```
Example 2:
```
Input: [1, 5, 3, 3]
Output: [], [1], [5], [3], [1,5], [1,3], [5,3], [1,5,3], [3,3], [1,3,3], [3,3,5], [1,5,3,3] 
```

This problem follows the Subsets pattern and we can follow a similar **Breadth First Search (BFS)** approach. The only additional thing we need to do is handle duplicates. Since the given set can have duplicate numbers, if we follow the same approach discussed in Subsets, we will end up with duplicate subsets, which is not acceptable. To handle this, we will do two extra things:

1. Sort all numbers of the given set. This will ensure that all duplicate numbers are next to each other.
2. Follow the same BFS approach but whenever we are about to process a duplicate (i.e., when the current and the previous numbers are same), instead of adding the current number (which is a duplicate) to all the existing subsets, only add it to the subsets which were created in the previous step.

Let’s take Example-2 mentioned above to go through each step of our algorithm:

```
Given set: [1, 5, 3, 3]  
Sorted set: [1, 3, 3, 5]
```

1. Start with an empty set: `[[]]`
2. Add the first number (1) to all the existing subsets to create new subsets: `[[], [1]]`;
3. Add the second number (3) to all the existing subsets: `[[], [1], [3], [1,3]]`.
4. The next number (3) is a duplicate. If we add it to all existing subsets we will get:
```
    [[], [1], [3], [1,3], [3], [1,3], [3,3], [1,3,3]]
```
```
We got two duplicate subsets: [3], [1,3]  
Whereas we only needed the new subsets: [3,3], [1,3,3]  
```

To handle this instead of adding (3) to all the existing subsets, we only add it to the new subsets which were created in the previous (3rd) step: ` [[], [1], [3], [1,3], [3,3], [1,3,3]]`


5. Finally, add the forth number (5) to all the existing subsets: `[[], [1], [3], [1,3], [3,3], [1,3,3], [5], [1,5], [3,5], [1,3,5], [3,3,5], [1,3,3,5]]`

<img width="882" alt="Screen Shot 2022-07-18 at 20 08 07" src="https://user-images.githubusercontent.com/103771536/179637197-539d6cf2-c59c-4a92-8c8b-4fe9385a39d3.png">









