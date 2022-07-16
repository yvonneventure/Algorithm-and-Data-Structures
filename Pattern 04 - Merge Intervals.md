# Merge Intervals

This pattern describes an efficient technique to deal with overlapping intervals. In a lot of problems involving intervals, we either need to find overlapping intervals or merge intervals if they overlap.

Given two intervals (‘a’ and ‘b’), there will be **six** different ways the two intervals can relate to each other:


<img width="454" alt="Screen Shot 2022-07-16 at 09 49 45" src="https://user-images.githubusercontent.com/103771536/179357666-6e2d010d-c091-4b1d-8879-ec7f9e3a8b5a.png">


### Problem - [Merge Intervals - Medium](https://leetcode.com/problems/merge-intervals/)

> Given a list of intervals, merge all the overlapping intervals to produce a list that has only mutually exclusive intervals.

Example 1:
```
Intervals: [[1,4], [2,5], [7,9]]
Output: [[1,5], [7,9]]
Explanation: Since the first two intervals [1,4] and [2,5] overlap, we merged them into 
one [1,5].
```
<img width="650" alt="Screen Shot 2022-07-16 at 09 53 01" src="https://user-images.githubusercontent.com/103771536/179357801-ef6eadc3-0470-4abc-9f79-4ef2e2e526a3.png">

Example 2:
```
Intervals: [[6,7], [2,4], [5,9]]
Output: [[2,4], [5,9]]
Explanation: Since the intervals [6,7] and [5,9] overlap, we merged them into one [5,9].
```

Example 3:
```
Intervals: [[1,4], [2,6], [3,5]]
Output: [[1,6]]
Explanation: Since all the given intervals overlap, we merged them into one.
```

Let’s take the example of two intervals (‘a’ and ‘b’) such that `a.start <= b.start`. There are four possible scenarios:

<img width="567" alt="Screen Shot 2022-07-16 at 09 57 05" src="https://user-images.githubusercontent.com/103771536/179357932-91591353-4195-4544-b630-fffc6594b97b.png">

Our goal is to merge the intervals whenever they overlap. For the above-mentioned three overlapping scenarios (2, 3, and 4), this is how we will merge them:

<img width="573" alt="Screen Shot 2022-07-16 at 09 57 35" src="https://user-images.githubusercontent.com/103771536/179357949-69813cb7-bee6-4089-90a2-c95eac45cc6a.png">

The diagram above clearly shows a merging approach. Our algorithm will look like this:

1. Sort the intervals on the start time to ensure `a.start <= b.start`
2. If ‘a’ overlaps ‘b’ (i.e.` b.start <= a.end`), we need to merge them into a new interval ‘c’ such that:

```
 c.start = a.start
 c.end = max(a.end, b.end)
 ```
 3. We will keep repeating the above two steps to merge ‘c’ with the next interval if it overlaps with ‘c’.


















