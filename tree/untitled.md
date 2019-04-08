# 250. Count Univalue Subtrees

## Question

> Given a binary tree, count the number of uni-value subtrees.
>
> A Uni-value subtree means all nodes of the subtree have the same value.
>
> **Example :**
>
> ```text
> Input:  root = [5,1,5,5,5,null,5]
>
>               5
>              / \
>             1   5
>            / \   \
>           5   5   5
>
> Output: 4
> ```

## Analysis

#### Solution \#1: Recursive

Define a recursive function to return whether the subtree is unival and also the value:

1. If the subtree is unival, return value;
2. If the subtree is null, return null;
3. If the subtree is not unival, return '!'

Time complexity would be `O(n)`.

## Code

```text
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var countUnivalSubtrees = function(root) {
  let count = 0;
  
  const isUnival = node => {
    if (!node) return null;
    
    // returns the left tree value, null or '!'
    const left = isUnival(node.left) || node.val;
    const right = isUnival(node.right) || node.val;
    
    if (node.val == left && node.val == right) {
      count += 1;
      return node.val;
    }
    
    return '!';
  };
  
  isUnival(root);
  return count;
};
```

