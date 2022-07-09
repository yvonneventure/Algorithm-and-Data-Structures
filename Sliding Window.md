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

**Time complexity**: Since for every element of the input array, we are calculating the sum of its next ‘K’ elements, the time complexity of the above algorithm will be O(N∗K) where ‘N’ is the number of elements in the input array and K is the size of the window.

Can we find a better solution? Do you see any inefficiency in the above approach?

The inefficiency is that for any two consecutive subarrays of size ‘5’, the overlapping part (which will contain four elements) will be evaluated twice. For example, take the above-mentioned input:


<img width="474" alt="Screen Shot 2022-07-09 at 10 14 55" src="https://user-images.githubusercontent.com/103771536/178109591-93ee3946-6a02-41b9-908a-79d1448f3fe1.png">

As you can see, there are four overlapping elements between the subarray (indexed from 0-4) and the subarray (indexed from 1-5). Can we somehow reuse the sum we have calculated for the overlapping elements?

The efficient way to solve this problem would be to visualize each contiguous subarray as a sliding window of ‘5’ elements. This means that when we move on to the next subarray, we will slide the window by one element. So, to reuse the sum from the previous subarray, we will subtract the element going out of the window and add the element now being included in the sliding window. This will save us from going through the whole subarray to find the sum and, as a result, the algorithm complexity will reduce to **O(N)**.

<img width="877" alt="Screen Shot 2022-07-09 at 10 15 46" src="https://user-images.githubusercontent.com/103771536/178109624-a7253324-5f33-4e61-9ec6-189b7df8e8ca.png">




