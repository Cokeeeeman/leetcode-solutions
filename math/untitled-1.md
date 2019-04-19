# 268. Missing Number

## Question

> Given an array containing n distinct numbers taken from `0, 1, 2, ..., n`, find the one that is missing from the array.
>
> **Example 1:**
>
> ```text
> Input: [3,0,1]
> Output: 2
> ```
>
> **Example 2:**
>
> ```text
> Input: [9,6,4,2,3,5,7,0,1]
> Output: 8
> ```
>
> **Note**:  
> Your algorithm should run in linear runtime complexity. Could you implement it using only constant extra space complexity?

## Analysis

#### Solution \#1: Use negative as flags

If we see a number `num`, we can mark the number `nums[num]` negative to indicate `num` is present.

To handle the case 0\(we can mark 0 negative\), we could use an additional variable to indicate whether 0 is found.

Time complexity would be `O(n)`.

#### Solution \#2: Bit Manipulation

We can make use XOR:

1. Any number XOR itself is 0;
2. Any number XOR 0 is itself;

We know that numbers are from \[0, n\], so we'll XOR \[0, n\] and then all numbers.

Time complexity would be`O(n)`.

#### Solution \#**3**: **Gauss' Formula**

Ref: [https://leetcode.com/problems/missing-number/solution/](https://leetcode.com/problems/missing-number/solution/)

## Code

#### Solution \#1: Use negative as flags

```text
/**
 * @param {number[]} nums
 * @return {number}
 */
var missingNumber = function(nums) {
  let zeroFound = false;
  for (let i = 0; i < nums.length; i++) {
    const num = Math.abs(nums[i]);
    if (num < nums.length) {
      if (nums[num] === 0) {
        zeroFound = true;
      }
      nums[num] *= -1;
    }
  }
  for (let i = 0; i < nums.length; i++) {
    if (nums[i] > 0) {
      return i;
    }
    
    if (nums[i] === 0 && !zeroFound) return i;
  }
  
  return nums.length;
};
```

#### Solution \#2: Bit Manipulation

```text
/**
 * @param {number[]} nums
 * @return {number}
 */
var missingNumber = function(nums) {
  return nums.length ^ nums.reduce((accum, num, index) => {
    return accum ^ num ^ index;
  }, 0);
};
```

#### Solution \#3: Gauss Formula

```text
/**
 * @param {number[]} nums
 * @return {number}
 */
var missingNumber = function(nums) {
  return nums.reduce((accum, num) => {
    return accum - num;
  }, nums.length * (nums.length + 1) / 2);
};
```

