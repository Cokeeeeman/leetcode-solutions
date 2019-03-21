# 31. Next Permutation

## Question

> Implement **next permutation**, which rearranges numbers into the lexicographically next greater permutation of numbers.
>
> If such arrangement is not possible, it must rearrange it as the lowest possible order \(ie, sorted in ascending order\).
>
> The replacement must be [**in-place**](http://en.wikipedia.org/wiki/In-place_algorithm) and use only constant extra memory.
>
> Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.
>
> `1,2,3` → `1,3,2`  
> `3,2,1` → `1,2,3`  
> `1,1,5` → `1,5,1`

## Analysis

```text
e.g. input is [ 1, 2, 3, 6, 5, 4 ]
```

1 - Scan array from right to left, find the 1st number that's not ascending. This is the first digit that can be increasable counting from right. Apparently 6, 5, 4 is the biggest out of all the combinations.

```text
[ 1, 2, [3], 6, 5, 4 ]
```

2 - Scan again from right to left, find the first number bigger than 3.

```text
[ 1, 2, [3], 6, 5, [4] ]
```

3 - Swap them

```text
[ 1, 2, [4], 6, 5, [3] ]
```

4 - Reverse all digits after 4.

```text
[ 1, 2, 4, 3, 5, 6 ]
```

## Code



```text
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var nextPermutation = function(nums) {
  // first digit that's increasable counting from right to left
  // e.g. 1, 2, [3], 6, 5, 4
  let idx1;
  for (let i = nums.length - 2; i >= 0; i -= 1) {
    if (nums[i] < nums[i + 1]) {
      idx1 = i;
      break;
    }
  }
  if (idx1 === undefined) {
    return reverse(nums, 0, nums.length - 1);
  }
  
  // find the 1st number that's bigger than idx1 from right to left
  let idx2 = nums.length - 1;
  while (idx2 > idx1) {
    if (nums[idx2] > nums[idx1]) {
      break;
    }
    idx2 -= 1;
  }
  
  swap(nums, idx1, idx2);
  reverse(nums, idx1 + 1, nums.length - 1);
};

var swap = (nums, i, j) => {
  let tmp = nums[i];
  nums[i] = nums[j];
  nums[j] = tmp;
};

var reverse = (nums, i, j) => {
  while (i < j) {
    swap(nums, i, j);
    i += 1;
    j -= 1;
  }
};
```

