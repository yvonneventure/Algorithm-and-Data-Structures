# Two Pointers

In problems where we deal with sorted arrays (or LinkedLists) and need to find a set of elements that fulfill certain constraints, the Two Pointers approach becomes quite useful. The set of elements could be a pair, a triplet or even a subarray. For example, take a look at the following problem:

> Given an array of sorted numbers and a target sum, find a pair in the array whose sum is equal to the given target.

To solve this problem, we can consider each element one by one (pointed out by the first pointer) and iterate through the remaining elements (pointed out by the second pointer) to find a pair with the given sum. The time complexity of this algorithm will be O(N^2) where ‘N’ is the number of elements in the input array.

Given that the input array is sorted, an efficient way would be to start with one pointer in the beginning and another pointer at the end. At every step, we will see if the numbers pointed by the two pointers add up to the target sum. If they do not, we will do one of two things:

- If the sum of the two numbers pointed by the two pointers is greater than the target sum, this means that we need a pair with a smaller sum. So, to try more pairs, we can decrement the end-pointer.
- If the sum of the two numbers pointed by the two pointers is smaller than the target sum, this means that we need a pair with a larger sum. So, to try more pairs, we can increment the start-pointer.

Here is the visual representation of this algorithm:

<img width="618" alt="Screen Shot 2022-07-09 at 14 38 54" src="https://user-images.githubusercontent.com/103771536/178118755-0607d7b8-81e6-45af-b683-cbef190dd0ce.png">

The time complexity of the above algorithm will be O(N).

### Problem : Pair with Target Sum - Easy

> Given an array of sorted numbers and a target sum, find a pair in the array whose sum is equal to the given target. Write a function to return the indices of the two numbers (i.e. the pair) such that they add up to the given target.

Example 1:
```
Input: [1, 2, 3, 4, 6], target=6
Output: [1, 3]
Explanation: The numbers at index 1 and 3 add up to 6: 2+4=6
```
Example 2:
```
Input: [2, 5, 9, 11], target=11
Output: [0, 2]
Explanation: The numbers at index 0 and 2 add up to 11: 2+9=11
```
My code:
```python
def pair_with_target_sum(arr,S):
  left=0
  right=len(arr)-1
  while left<right:
    addition=arr[left]+arr[right]
    if addition==S:
      return print([left,right])
    if addition>S:
      right-=1
    else:
      left+=1
  return print([-1,-1])
   

pair_with_target_sum([1, 2, 3, 4, 6],6)
pair_with_target_sum([2, 5, 9, 11],11)
```

#### Time Complexity #
The time complexity of the above algorithm will be O(N), where ‘N’ is the total number of elements in the given array.

#### Space Complexity #
The algorithm runs in constant space O(1).






















