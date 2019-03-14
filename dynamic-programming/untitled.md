# 121. Best Time to Buy and Sell Stock

## Question

> Say you have an array for which the _i_th element is the price of a given stock on day _i_.
>
> If you were only permitted to complete at most one transaction \(i.e., buy one and sell one share of the stock\), design an algorithm to find the maximum profit.
>
> Note that you cannot sell a stock before you buy one.
>
> **Example 1:**
>
> ```text
> Input: [7,1,5,3,6,4]
> Output: 5
> Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
>              Not 7-1 = 6, as selling price needs to be larger than buying price.
> ```
>
> **Example 2:**
>
> ```text
> Input: [7,6,4,3,1]
> Output: 0
> Explanation: In this case, no transaction is done, i.e. max profit = 0.
> ```

## Analysis

Let's break it down to smaller problems:

Let `dp[i]` be the max profit selling stock at point `i`. Then the final result would be the max among `dp[i]`. 

To calculate `dp[i]`, we just need to track the min stock before `i`.

So the algorithm is:

1. Iterate thru the array from left to right;
2. Keep track of the min stock ending at index `i`;
3. Calculate the local max profit at index `i`;
4. Keep updating the global max profit.

Time complexity: `O(n)`.

{% hint style="info" %}
This is similar to 53. Maximum Subarray.
{% endhint %}

#### 

## Code

```text
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
  if (prices.length === 0) return 0;

  let maxProfit = 0;
  let min = prices[0];
  for (let i = 1; i < prices.length; i++) {
    min = Math.min(prices[i], min);
    maxProfit = Math.max(prices[i] - min, maxProfit);
  }
  
  return maxProfit;
};
```

