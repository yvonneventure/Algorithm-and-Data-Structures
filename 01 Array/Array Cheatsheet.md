# Array Cheatsheet

Arrays hold values of the **same type** at **contiguous memory locations**. 

### Difference of Array and List in Python

- List is built in, and array needs import
- An array is faster than a list in python since all the elements stored in an array are homogeneous (they have the same data type), whereas a list contains heterogeneous elements.
- Python arrays are implemented in C which makes it a lot faster than lists that are built-in in Python itself.
- Array has a fixed sized and cannot resize (need to be copied to a bigger array), whereas list can be resized.

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

#### - Sliding Window













