# Sliding Window

In many problems dealing with an array (or a LinkedList), we are asked to find or calculate something among all the contiguous subarrays (or sublists) of a given size. For example, take a look at this problem:

> Given an array, find the average of all contiguous subarrays of size ‘K’ in it. 
> Let’s understand this problem with a real input: `Array: [1, 3, 2, 6, -1, 4, 1, 8, 2], K=5`


<img width="331" alt="Screen Shot 2022-07-09 at 09 59 32" src="https://user-images.githubusercontent.com/103771536/178109008-e7e30e05-de62-42eb-8091-384a7787325c.png">

Here, we are asked to find the average of all contiguous subarrays of size ‘5’ in the given array. Let’s solve this:

- For the first 5 numbers (subarray from index 0-4), the average is: `(1+3+2+6-1)/5 => 2.2(1+3+2+6−1)/5=>2.2`
- The average of next 5 numbers (subarray from index 1-5) is: `(3+2+6-1+4)/5 => 2.8(3+2+6−1+4)/5=>2.8`

...

Here is the final output containing the averages of all contiguous subarrays of size 5: `Output: [2.2, 2.8, 2.4, 3.6, 2.8]`


A **brute-force algorithm** will be to calculate the sum of every 5-element contiguous subarray of the given array and divide the sum by ‘5’ to find the average. This is what the algorithm will look like:

```python

def find_average(arr,K):
  end_result=[]
  
  for i in range(len(arr)-K+1):
    sum=0
    for j in range(i+K):
      sum+=arr[j]
    end_result.append(sum/K)
  return print(f'Averages of subarrays of size K: {end_result}')


find_average([1, 3, 2, 6, -1, 4, 1, 8, 2], 5)

# output - Averages of subarrays of size K: [2.2, 2.8, 2.4, 3.6, 2.8]
```

**Time complexity**: Since for every element of the input array, we are calculating the sum of its next ‘K’ elements, the time complexity of the above algorithm will be **O(N∗K)** where ‘N’ is the number of elements in the input array and K is the size of the window.

Can we find a better solution? Do you see any inefficiency in the above approach?

The inefficiency is that for any two consecutive subarrays of size ‘5’, the overlapping part (which will contain four elements) will be evaluated twice. For example, take the above-mentioned input:


<img width="474" alt="Screen Shot 2022-07-09 at 10 14 55" src="https://user-images.githubusercontent.com/103771536/178109591-93ee3946-6a02-41b9-908a-79d1448f3fe1.png">

As you can see, there are four overlapping elements between the subarray (indexed from 0-4) and the subarray (indexed from 1-5). Can we somehow reuse the sum we have calculated for the overlapping elements?

The efficient way to solve this problem would be to visualize each contiguous subarray as a sliding window of ‘5’ elements. This means that when we move on to the next subarray, we will slide the window by one element. So, to reuse the sum from the previous subarray, we will subtract the element going out of the window and add the element now being included in the sliding window. This will save us from going through the whole subarray to find the sum and, as a result, the algorithm complexity will reduce to **O(N)**.

<img width="877" alt="Screen Shot 2022-07-09 at 10 15 46" src="https://user-images.githubusercontent.com/103771536/178109624-a7253324-5f33-4e61-9ec6-189b7df8e8ca.png">

Here's the algorithm: form the window and adding elements, when window size hits, do the calculation then slide the window

```python
def find_average(arr,K):
  end_result=[]
  window_start=0
  window_sum=0
  for window_end in range(len(arr)):
    window_sum+=arr[window_end] #adding the next element
    # slide the window, we don't need to slide the window if we are not hitting the window size K
    if window_end>=K-1:
      end_result.append(window_sum/K)
      window_sum-=arr[window_start] # subtract first element
      window_start+=1 #slide the window ahead
      
  return print(f'average array is {end_result}')


find_average([1, 3, 2, 6, -1, 4, 1, 8, 2], 5)
```

### Problem : [Maximum Sum Subarray of Size K - Easy](https://leetcode.com/problems/maximum-subarray/)

> Given an array of positive numbers and a positive number ‘k’, find the maximum sum of any contiguous subarray of size ‘k’.

Example 1:
```
Input: [2, 1, 5, 1, 3, 2], k=3 
Output: 9
Explanation: Subarray with maximum sum is [5, 1, 3].
```

Example 2:
```
Input: [2, 3, 4, 1, 5], k=2 
Output: 7
Explanation: Subarray with maximum sum is [3, 4].
```

My Code: 

```python

def find_maxsum(arr,K):
  end_result=[]
  window_start=0
  window_sum=0
  max_sum=0
  for window_end in range(len(arr)):
    window_sum+=arr[window_end] #adding the next element
   
    if window_end>=K-1:
      if window_sum>max_sum:
        max_sum=window_sum      ## can also use max_sum=max(max_sum,window_sum) to updated max_sum, but won't get the subarray
        end_result=arr[window_start:window_end+1]
      window_sum-=arr[window_start] # subtract first element
      window_start+=1 #slide the window ahead
      
  return print(f'Explanation: Subarray with maximum sum is {end_result} \nOutput is {max_sum}')


find_maxsum([2, 1, 5, 1, 3, 2], 3)
find_maxsum([2, 3, 4, 1, 5], 2)
```

##### Time Complexity #
The time complexity of the above algorithm will be O(N).

##### Space Complexity #
The algorithm runs in constant space O(1).


### Problem : [Smallest Subarray with a given sum - Easy](https://leetcode.com/problems/minimum-size-subarray-sum/)

> Given an array of positive numbers and a positive number ‘S’, find the length of the smallest contiguous subarray whose sum is greater than or equal to ‘S’. **Return 0, if no such subarray exists**.

This problem follows the Sliding Window pattern, however, **the size of the sliding window is not fixed**. 

Here is how we will solve this problem:

1. First, we will add-up elements from the beginning of the array until their sum becomes greater than or equal to ‘S’.
These elements will constitute our sliding window. We are asked to find the smallest such window having a sum greater than or equal to ‘S’. We will remember the length of this window as the smallest window so far.
2. After this, we will keep adding one element in the sliding window (i.e. slide the window ahead), in a stepwise fashion.
3. In each step, we will also try to shrink the window from the beginning. We will shrink the window until the window’s sum is smaller than ‘S’ again. This is needed as we intend to find the smallest window. This shrinking will also happen in multiple steps; in each step we will do two things:
  - Check if the current window length is the smallest so far, and if so, remember its length.
  - Subtract the first element of the window from the running sum to shrink the sliding window.

Here is the visual representation of this algorithm for the Example-1

<img width="424" alt="Screen Shot 2022-07-09 at 11 05 06" src="https://user-images.githubusercontent.com/103771536/178111345-20fbc920-8d72-4274-a9aa-d277c070f542.png">

<img width="414" alt="Screen Shot 2022-07-09 at 11 05 25" src="https://user-images.githubusercontent.com/103771536/178111357-709f088d-e881-44d4-87e3-66541def2999.png">

<img width="392" alt="Screen Shot 2022-07-09 at 11 05 51" src="https://user-images.githubusercontent.com/103771536/178111371-f0688716-8073-4955-ac86-537c864f95bb.png">

My code:

```python
import math

def find_smallest_subarray_with_given_sum(arr,S):
  end_result=[]
  window_start=0
  window_sum=0
  min_len=math.inf  ## first set the length to infinity
  
  for window_end in range(len(arr)):
    window_sum+=arr[window_end] 
    while window_sum>=S:  ## when window sum is greater than or equal to the given sum, record the min_len, then substract the first element and moving the window ahead
      if len(arr[window_start:window_end+1])<=min_len:
        end_result=arr[window_start:window_end+1]
        min_len=len(end_result)  
      window_sum-=arr[window_start] # subtract first element
      window_start+=1 #slide the window ahead
  if min_len==math.inf:  ## if no such subarray exists
    return print(0)
  return print(f'Explanation: Subarray with given sum {S} is {end_result} \nMinimum length is {min_len}')


find_smallest_subarray_with_given_sum([2, 1, 5, 2, 3, 2], 7)
find_smallest_subarray_with_given_sum([2, 1, 5, 2, 8], 7)
find_smallest_subarray_with_given_sum([3, 4, 1, 1, 6], 8)
find_smallest_subarray_with_given_sum([3, 4, 1, 1, 6], 50)
```

##### Time Complexity #
The time complexity of the above algorithm will be O(N). The outer for loop runs for all elements and the inner while loop processes each element only once, therefore the time complexity of the algorithm will be O(N+N) which is asymptotically equivalent to O(N).

##### Space Complexity #
The algorithm runs in constant space O(1).


### Problem: Longest Substring with K Distinct Characters - Medium

> Given a string, find the length of the longest substring in it with no more than K distinct characters.

Example 1:
```
Input: String="araaci", K=2
Output: 4
Explanation: The longest substring with no more than '2' distinct characters is "araa".
```

Example 2:
```
Input: String="araaci", K=1
Output: 2
Explanation: The longest substring with no more than '1' distinct characters is "aa".
```
Example 3:
```
Input: String="cbbebi", K=3
Output: 5
Explanation: The longest substrings with no more than '3' distinct characters are "cbbeb" & "bbebi".
```

This problem follows the Sliding Window pattern and we can use a similar dynamic sliding window strategy as discussed in Smallest Subarray with a given sum. We can use a **HashMap** to remember the frequency of each character we have processed. 

Here is how we will solve this problem:

1. First, we will insert characters from the beginning of the string until we have ‘K’ distinct characters in the HashMap.
2. These characters will constitute our sliding window. We are asked to find the longest such window having no more than ‘K’ distinct characters. We will remember the length of this window as the longest window so far.

3. After this, we will keep adding one character in the sliding window (i.e. slide the window ahead), in a stepwise fashion.
4. In each step, we will try to shrink the window from the beginning if the count of distinct characters in the HashMap is larger than ‘K’. We will shrink the window until we have no more than ‘K’ distinct characters in the HashMap. This is needed as we intend to find the longest window.
5. While shrinking, we’ll decrement the frequency of the character going out of the window and remove it from the HashMap if its frequency becomes zero.
6. At the end of each step, we’ll check if the current window length is the longest so far, and if so, remember its length.

Here is the visual representation of this algorithm for the Example-1:

<img width="394" alt="Screen Shot 2022-07-09 at 11 48 16" src="https://user-images.githubusercontent.com/103771536/178112924-072db4c7-3be9-4129-8f04-b08b9bdd0a63.png">

<img width="424" alt="Screen Shot 2022-07-09 at 11 48 41" src="https://user-images.githubusercontent.com/103771536/178112939-6ed65dd6-9d9b-471b-a8b9-a7767fb0b0dc.png">
<img width="415" alt="Screen Shot 2022-07-09 at 11 49 02" src="https://user-images.githubusercontent.com/103771536/178112958-90e9b7fa-e3fe-490f-b286-223e6ff09a02.png">

My code:

```python
def find_longest_substring_with_distinct_chars(str,K):
  window_start=0
  chars={}
  max_len=0
  ## for loop here is to add elements in window/hashmap with window start unchanged
  # str_end is the end/right letter of the window string
  # window_end is the index of the end/right letter of the window string
  for window_end in range(len(str)):
    str_end=str[window_end]   
    if str_end not in chars:
      chars[str_end]=0
    chars[str_end]+=1
  ## while loop is to check the constraint, record the current result and shrink the window string
    while len(chars)>K:
      if window_end- window_start>=max_len:
        result=str[window_start:window_end]
        max_len=window_end- window_start
      str_start=str[window_start]
      chars[str_start]-=1
      if chars[str_start]==0:
        del chars[str_start]
      window_start+=1
  
  return print(f'Explanation: substring with longest K distinct characters is {result} \nMaximum Length is {max_len}')

find_longest_substring_with_distinct_chars("araaci",2)
find_longest_substring_with_distinct_chars("araaci",1)
find_longest_substring_with_distinct_chars("cbbebi",3)
```

#### Time Complexity #
The time complexity of the above algorithm will be O(N) where ‘N’ is the number of characters in the input string. The outer for loop runs for all characters and the inner while loop processes each character only once, therefore the time complexity of the algorithm will be O(N+N) which is asymptotically equivalent to O(N).

#### Space Complexity #
The space complexity of the algorithm is O(K), as we will be storing a maximum of ‘K+1’ characters in the HashMap.


### Probelm: [No-repeat Substring - Hard](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

> Given a string, find the length of the longest substring which has no repeating characters.

Example 1:
```
Input: String="aabccbb"
Output: 3
Explanation: The longest substring without any repeating characters is "abc".
```
Example 2:
```
Input: String="abbbb"
Output: 2
Explanation: The longest substring without any repeating characters is "ab".
```
Example 3:
```
Input: String="abccde"
Output: 3
Explanation: Longest substrings without any repeating characters are "abc" & "cde".
```

This problem follows the Sliding Window pattern and we can use a similar dynamic sliding window strategy as discussed in Longest Substring with K Distinct Characters.

We can use a **HashMap** to remember the last **index** of each character we have processed. Whenever we get a repeating character we will shrink our sliding window to ensure that we always have distinct characters in the sliding window.

 ```python
 
def find_nonrepeat_substring(str):
  window_start=0
  chars={}
  max_len=0
 ## move window-end one by one
  for window_end in range(len(str)):
    str_end=str[window_end]   
    
    ## check if the charater is already in the hashmap
    
    if str_end in chars:  # if it's in the hashmap, meaning we have a duplicate, shrink the window by moving window start one step ahead of it's last appearance
      window_start=max(window_start,chars[str_end]+1)
      
    #if not there, meaning the first time, add the letter and it's index into the hashmap
     #whether if exists or not, the index of the str_end will be updated 
    chars[str_end]=window_end
    
    ## only update the end result when the substring length is longer than the last satisfied substring
    if window_end-window_start+1>max_len:
     max_len=window_end-window_start+1
     result=str[window_start:window_end+1] 
  
  
  return print(f'Explanation: substring with longest nonrepeating characters is {result} \nMaximum Length is {max_len}')

find_nonrepeat_substring("aabccbb")
find_nonrepeat_substring("abbbb")
find_nonrepeat_substring("abccde")
```

> Use step through to see the execution order https://pythontutor.com/render.html#mode=display

#### Time Complexity #
The time complexity of the above algorithm will be O(N) where ‘N’ is the number of characters in the input string.

#### Space Complexity #
The space complexity of the algorithm will be O(K) where K is the number of distinct characters in the input string. This also means K<=N, because in the worst case, the whole string might not have any repeating character so the entire string will be added to the HashMap. Having said that, since we can expect a fixed set of characters in the input string (e.g., 26 for English letters), we can say that the algorithm runs in fixed space O(1); in this case, we can use a fixed-size array instead of the HashMap.

































