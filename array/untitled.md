# 15. 3Sum

## Question

> Given an array `nums` of _n_ integers, are there elements _a_, _b_, _c_ in `nums` such that _a_ + _b_ + _c_= 0? Find all unique triplets in the array which gives the sum of zero.
>
> **Note:**
>
> The solution set must not contain duplicate triplets.
>
> **Example:**
>
> ```text
> Given array nums = [-1, 0, 1, 2, -1, -4],
>
> A solution set is:
> [
>   [-1, 0, 1],
>   [-1, -1, 2]
> ]
> ```

## Analysis

#### Solution \#1: Brute force

It's gonna be 3 level nested loops, time would cubic.

#### Solution \#2: **Two Pointers**. 

We'll have to sort the array first for this solution, which will take `O(nlogn)`. We iterate thru the array with index `i`, this is the outer loop. When `i` is fixed, for the rest of the array, we set 2 pointers `j` and `k` at the start and end of the array.  We sum up 3 numbers at this time:

* if the sum is larger than 0, we'll make sum smaller by moving `k` to the left \(because the array is sorted\);
* if the sum is smaller than 0, we'll make sum bigger by moving `j` to the right;
* if the sum is 0, put triplets in the final result.

So time complexity would be `O(n^2)`.

{% hint style="warning" %}
Be careful with duplicates
{% endhint %}

## Code

#### Javascript

```text
/**
 * Solution #2
 * Time complexity: O(n^2)
 * @param {number[]} nums
 * @return {number[][]}
 */
var threeSum = function(nums) {
  const result = [];
    
  // sort the array for 2 pointers
  nums.sort((a, b) => a - b);
    
  for (let i = 0; i < nums.length - 2; i++) {  
    // avoid duplicates
    if (i > 0 && nums[i] === nums[i - 1]) continue;

    let j = i + 1;
    let k = nums.length - 1;
    
    // 2 pointers
    while (j < k) {
      // avoid duplicates
      if (j > i + 1 && nums[j] === nums[j - 1]) {
        j += 1;
        continue;
      }
      // avoid duplicates
      if (k < nums.length - 1 && nums[k] === nums[k + 1]) {
        k -= 1;
        continue;
      }
  
      const sum = nums[i] + nums[j] + nums[k];
      if (sum === 0) {
        result.push([nums[i], nums[j], nums[k]]);
        k -= 1;
        j += 1;
      } else if (sum > 0) {
        k -= 1;
      } else {
        j += 1;
      }
    }
  }
  
  return result;
};
```

