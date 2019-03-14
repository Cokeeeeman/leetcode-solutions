# Background Knowledge

## Insertion Sort

### How it works

![](https://upload.wikimedia.org/wikipedia/commons/0/0f/Insertion-sort-example-300px.gif)  
A graphical example of insertion sort. The partial sorted list \(black\) initially contains only the first element in the list.  
With each iteration one element \(red\) is removed from the input data and inserted in-place into the sorted list

**Algorithm of Insertion Sort:**

1. Insertion sort iterates, consuming one input element each repetition, and growing a sorted output list.
2. At each iteration, insertion sort removes one element from the input data, finds the location it belongs within the sorted list, and inserts it there.
3. It repeats until no input elements remain.

**Time Complexity:** `O(n^2)`

### Code

```text
/**
 * Insertion sort
 * @param  {Number[]} array Input array
 * @return {Number[]}       Sorted array
 */
const insertionSort = array => {
  if (!array) {
    throw new Error('Missing param: array');
  }

  for (let i = 1; i < array.length; i++) {
    for (let j = i - 1; j >= 0; j--) {
      if (array[j] > array[j + 1]) {
        const tmp = array[j + 1];
        array[j + 1] = array[j];
        array[j] = tmp;
      }
    }
  }

  return array;
};
```

## Merge Sort

### How it works

**Time Complexity:** `O(nlogn)`

### Code

```text
/**
 * Merge two arrays into one
 * @param  {Number[]} arr1
 * @param  {Number[]} arr2
 * @return {Number[]} merged
 */
const merge = (arr1, arr2) => {
  const merged = [];

  let p1 = 0;
  let p2 = 0;

  while (p1 < arr1.length && p2 < arr2.length) {
    if (arr1[p1] < arr2[p2]) {
      merged.push(arr1[p1]);
      p1 += 1;
    } else {
      merged.push(arr2[p2]);
      p2 += 1;
    }
  }

  merged.push(...arr1.slice(p1), ...arr2.slice(p2));
  return merged;
};

/**
 *  * Merge sort
 * @param  {Number[]} array Input array
 * @return {Number[]}       Sorted array
 */
const mergeSort = array => {
  if (!array) {
    throw new Error('Missing param: array');
  }

  if (array.length < 2) {
    return array.slice(0);
  }

  const left = 0;
  const right = array.length - 1;
  const middle = Math.floor((left + right) / 2);

  const leftArray = array.slice(left, middle + 1);
  const rightArray = array.slice(middle + 1);

  return merge(mergeSort(leftArray), mergeSort(rightArray));
};
```



