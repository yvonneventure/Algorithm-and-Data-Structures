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


### Problem: Remove Duplicates - Easy

> Given an array of sorted numbers, remove all duplicates from it. You should not use any extra space; after removing the duplicates in-place return the new length of the array.

Example 1:
```
Input: [2, 3, 3, 3, 6, 9, 9]
Output: 4
Explanation: The first four elements after removing the duplicates will be [2, 3, 6, 9].
```

Example 2:
```
Input: [2, 2, 2, 11]
Output: 2
Explanation: The first two elements after removing the duplicates will be [2, 11].
```

As the input array is sorted, therefore, one way to do this is to shift the elements left whenever we encounter duplicates. In other words, we will keep one pointer for iterating the array and one pointer for placing the next non-duplicate number. So our algorithm will be to iterate the array and whenever we see a non-duplicate number we move it next to the last non-duplicate number we’ve seen.

<img width="422" alt="Screen Shot 2022-07-10 at 10 21 12" src="https://user-images.githubusercontent.com/103771536/178148885-475ce662-9b16-4821-bf33-d5e5c362c138.png">

My Code:

```python
def remove_duplicates(arr):
  right_pointer=1
  left_pointer=0
  while right_pointer<len(arr):
    if arr[right_pointer]==arr[right_pointer-1]:
      del arr[right_pointer]
    else:
      right_pointer+=1
      left_pointer+=1
   
  return print(f' length of the array is {left_pointer+1} and the array is {arr}')
remove_duplicates([2, 3, 3, 3, 6, 9, 9])
remove_duplicates([2, 2, 2, 11])
```

Solution Code:

```python
def remove_duplicates(arr):
    left_pointer = 1
    right_pointer = 1
    while right_pointer < len(arr):
        if arr[left_pointer - 1] != arr[right_pointer]:
            arr[left_pointer] = arr[right_pointer]
            left_pointer += 1

        right_pointer += 1

    return print(f' length of the array is {left_pointer}')
 ```
 
#### Time Complexity #

The time complexity of the above algorithm will be O(N), where ‘N’ is the total number of elements in the given array.

#### Space Complexity #

The algorithm runs in constant space O(1).

> Similar Questions # : Given an unsorted array of numbers and a target ‘key’, remove all instances of ‘key’ in-place and return the new length of the array.

Example 1:
```
Input: [3, 2, 3, 6, 3, 10, 9, 3], Key=3
Output: 4
Explanation: The first four elements after removing every 'Key' will be [2, 6, 10, 9].
```
Example 2:
```
Input: [2, 11, 2, 2, 1], Key=2
Output: 2
Explanation: The first two elements after removing every 'Key' will be [11, 1].
```

My code:
```python
def remove_keys(arr,K):
    left_pointer=0
    right_pointer = 0
    while right_pointer < len(arr):
        if arr[right_pointer]==K:
            del arr[right_pointer]


        else:
            right_pointer+=1
            left_pointer+=1

    return print(f' length of the array is {left_pointer} and array {arr}')


remove_keys([2, 3, 3, 3, 6, 9, 9],3)
remove_keys([2, 2, 2, 11],2)
```

Solution code:

```python
def remove_keys(arr,K):
    left_pointer=0
   
    for right_pointer in range(len(arr)):
        if arr[right_pointer]!= K:
           
            left_pointer+=1

    return print(f' length of the array is {left_pointer} and array {arr}')
```

### Problem : Squaring a Sorted Array - Easy

> Given a sorted array, create a new array containing squares of all the number of the input array in the sorted order.

Example 1:
```
Input: [-2, -1, 0, 2, 3]
Output: [0, 1, 4, 4, 9]
```
Example 2:
```
Input: [-3, -1, 0, 1, 2]
Output: [0, 1, 1, 4, 9]
```

This is a straightforward question. The only trick is that we can have negative numbers in the input array, which will make it a bit difficult to generate the output array with squares in sorted order.

An easier approach could be to first find the index of the first non-negative number in the array. After that, we can use Two Pointers to iterate the array. One pointer will move forward to iterate the non-negative numbers and the other pointer will move backward to iterate the negative numbers. At any step, whichever number gives us a bigger square will be added to the output array.

<img width="335" alt="Screen Shot 2022-07-10 at 11 07 23" src="https://user-images.githubusercontent.com/103771536/178150579-9f4ffbf9-3505-48c3-bb3d-c6e4bef4cc7a.png">

Since the numbers at both the ends can give us the largest square, an alternate approach could be to use two pointers starting at both the ends of the input array. At any step, whichever pointer gives us the bigger square we add it to the result array and move to the next/previous number according to the pointer.

<img width="302" alt="Screen Shot 2022-07-10 at 11 08 03" src="https://user-images.githubusercontent.com/103771536/178150607-52fa16a3-9a76-491f-adbf-b431f3ca7b5c.png">

```python
def make_squares(arr):
    n = len(arr)
    squares=[0 for x in range(n)]
    pointer= n-1
    left=0
    right=n-1
    while left<=right:
        leftsq=arr[left]*arr[left]
        rightsq = arr[right] * arr[right]
        if leftsq>rightsq:
            squares[pointer]=leftsq
            left+=1
        else:
            squares[pointer] = rightsq
            right-=1
        pointer-=1
    return print(f'squares array is {squares}')

make_squares([-2, 2, 3,])
make_squares([-1, 0, 2, 4])
```

#### Time complexity #
The time complexity of the above algorithm will be O(N) as we are iterating the input array only once.

#### Space complexity #
The space complexity of the above algorithm will also be O(N); this space will be used for the output array.


### Problem: [Triplet Sum to Zero - Medium](https://leetcode.com/problems/3sum/)

> Given an array of unsorted numbers, find all **unique triplets in it that add up to zero**.

Example 1:
```
Input: [-3, 0, 1, 2, -1, 1, -2]
Output: [-3, 1, 2], [-2, 0, 2], [-2, 1, 1], [-1, 0, 1]
Explanation: There are four unique triplets whose sum is equal to zero.
```
Example 2:
```
Input: [-5, 2, -1, -2, 3]
Output: [[-5, 2, 3], [-2, -1, 3]]
Explanation: There are two unique triplets whose sum is equal to zero.
```

This problem follows the **Two Pointers** pattern and shares similarities with **Pair with Target Sum**. A couple of differences are that the input array is not sorted and instead of a pair we need to find triplets with a target sum of zero.

To follow a similar approach, first, we will **sort** the array and then iterate through it taking one number at a time. Let’s say during our iteration we are at number ‘X’, so we need to find ‘Y’ and ‘Z’ such that X + Y + Z == 0X+Y+Z==0. At this stage, our problem translates into finding a pair whose sum is equal to “-X−X” (as from the above equation Y + Z == -XY+Z==−X).

Another difference from Pair with Target Sum is that we need to find all the **unique** triplets. To handle this, we have to skip any duplicate number. Since we will be sorting the array, so all the duplicate numbers will be next to each other and are easier to skip.

```python
def search_triplets(arr):
    arr.sort()
    triplets=[]
    for i in range(len(arr)):  ## skip the duplicates
        if i>0 and arr[i]==arr[i-1]:
            continue
        search_pair(arr,-arr[i],i+1,triplets)

    return print(f'array is {triplets}')

## search pairs with target sum
def search_pair(arr,target_sum,left,triplets):
    right=len(arr)-1
    while left<right:
        current_sum=arr[left]+arr[right]
        if current_sum==target_sum:   #foud the pair
            triplets.append([-target_sum,arr[left],arr[right]])
            left+=1
            right-=1
            while left<right and arr[left]==arr[left-1]: #skip the duplicte
                left+=1
            while left< right and arr[right]==arr[right+1]: #skip the duplicte
                right-=1
        elif target_sum>current_sum:
            left+=1
        else:
            right-=1


search_triplets([-3, 0, 1, 2, -1, 1, -2])
search_triplets([-5, 2, -1, -2, 3])
```

#### Time complexity #

Sorting the array will take O(N * logN)([Quick Sort]()). The `searchPair()` function will take O(N). As we are calling searchPair() for every number in the input array, this means that overall s`earchTriplets()` will take O(N * logN + N^2), which is asymptotically equivalent to O(N^2).

#### Space complexity #
Ignoring the space required for the output array, the space complexity of the above algorithm will be O(N) which is required for sorting.




### Problem: [Dutch National Flag Problem - Medium](https://leetcode.com/problems/sort-colors/)

> Given an array containing 0s, 1s and 2s, sort the array in-place. You should treat numbers of the array as objects, hence, we can’t count 0s, 1s, and 2s to recreate the array.
> 
> The flag of the Netherlands consists of three colors: red, white and blue; and since our input array also consists of three different numbers that is why it is called Dutch National Flag problem.

Example 1:
```
Input: [1, 0, 2, 1, 0]
Output: [0, 0, 1, 1, 2]
```
Example 2:
```
Input: [2, 2, 0, 1, 2, 0]
Output: [0, 0, 1, 2, 2, 2]
```

The brute force solution will be to use an in-place sorting algorithm like **Heapsort** which will take O(N*logN). Can we do better than this? Is it possible to sort the array in one iteration?

We can use a Two Pointers approach while iterating through the array. Let’s say the two pointers are called `low` and `high` which are pointing to the first and the last element of the array respectively. So while iterating, we will move all 0s before `low` and all 2s after `high` so that in the end, all 1s will be between `low` and `high`.

```python
def color_sort(arr):
    # all elements <low are 0, and all elements>high are 2
    # all elements from >= low <i are 1
    low=0
    high=len(arr)-1
    i=0
    while i<=high:
        if arr[i]==0:
            arr[i],arr[low]=arr[low],arr[i]
        # increment i and low
            i+=1
            low+=1
        elif arr[i]==1:
            i+=1
        else:
            arr[i],arr[high]=arr[high],arr[i]
            #decrement high only, after the swap, number at index i could be 0,1,2, so i should not be incremented
            high-=1

    return print(f'Sorted array is {arr}')

color_sort([1, 0, 2, 1, 0])
color_sort([2, 2, 0, 1, 2, 0])
```

#### Time complexity #
The time complexity of the above algorithm will be O(N) as we are iterating the input array only once.

#### Space complexity #
The algorithm runs in constant space O(1).


### Problem : [Palindromic Substrings - Medium](https://leetcode.com/problems/palindromic-substrings/)

### Problem : [Merge Sorted Array - Easy](https://leetcode.com/problems/merge-sorted-array/)























