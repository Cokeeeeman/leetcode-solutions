# 280. Wiggle Sort

## Question

> Given an unsorted array `nums`, reorder it **in-place** such that `nums[0] <= nums[1] >= nums[2] <= nums[3]...`.
>
> **Example:**
>
> ```text
> Input: nums = [3,5,2,1,6,4]
> Output: One possible answer is [3,5,1,6,2,4
> ```

## Analysis

#### [https://leetcode.com/problems/wiggle-sort/solution/](https://leetcode.com/problems/wiggle-sort/solution/)

## Code

#### Solution \#1

```text
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var wiggleSort = function(nums) {
  nums.sort((a, b) => a - b);
  
  for (let i = 1; i < nums.length - 1; i += 2) {
    swap(nums, i, i + 1);
  }
};

const swap = (nums, i, j) => {
  let temp = nums[i];
  nums[i] = nums[j];
  nums[j] = temp;
}
```

#### Solution \#2

```text
var wiggleSort = function(nums) {
  let less = true;
  for (let i = 0; i < nums.length - 1; i++) {
    if (less) {
      if (nums[i] > nums[i + 1]) {
        swap(nums, i, i + 1);
      }
    } else {
      if (nums[i] < nums[i + 1]) {
        swap(nums, i, i + 1);
      }
    }
    
    less = !less;
  }
};
```

