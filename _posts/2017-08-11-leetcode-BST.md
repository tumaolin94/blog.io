---
layout: post
title: Leetcode Some problems about Binary Search Tree 
date: 2017-08-03
categories: blog
tags: [Binary Tree, algorithm, BST]
description: 

---
# 173. Binary Search Tree Iterator
## Description
Implement an iterator over a binary search tree (BST). Your iterator will be initialized with the root node of a BST.

Calling `next()` will return the next smallest number in the BST.

Note: `next()` and `hasNext()` should run in average O(1) time and uses O(h) memory, where h is the height of the tree.

## Answer
We need a Stack to help us to save the next smallest number.

In a Binary Search Tree, The most left node is the minimum. So we can save each left node from root in a stack and get the minimum left node.
So the function `hasNext()` just return !stack.isEmpty();
And every time we use `next()`,we pop the stack, and push all left nodes of the pop node's right node.
So code is following.

```
public class BSTIterator {
    
    Stack<TreeNode> stack;
    public BSTIterator(TreeNode root) {
        stack = new Stack<>();
        while(root!=null){
            stack.push(root);
            root=root.left;
        }
    }

    /** @return whether we have a next smallest number */
    public boolean hasNext() {
        return !stack.isEmpty();
    }

    /** @return the next smallest number */
    public int next() {
        TreeNode min = stack.pop();
        TreeNode temp = min.right;
        
        while(temp!=null){
            stack.push(temp);
            temp=temp.left;
        }
        return min.val;
    }
}
```

# 98. Validate Binary Search Tree
## Description
Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and right subtrees must also be binary search trees.
Example 1:
```
    2
   / \
  1   3
```
Binary tree `[2,1,3]`, return true.
Example 2:
```
    1
   / \
  2   3
```
Binary tree `[1,2,3]`, return false.

## Answer
The basic method is to use a inorder traversal, because in a BST the left always less than the right.

I design a recursion to solve the problem.

```
public class Solution {
    long temp = Long.MIN_VALUE;
    public boolean isValidBST(TreeNode root) {
        if(root==null) return true;
        
        boolean left = isValidBST(root.left);
        if(temp<root.val){
            temp = root.val;
        }else{
            return false;
        }
        
        boolean right = isValidBST(root.right);
        
        return left&&right;
    }
}
```

# 108. Convert Sorted Array to Binary Search Tree
## Description
Given an array where elements are sorted in ascending order, convert it to a height balanced BST

## Answer

With what I said above, BST owns its special character, left < right. So the middle of the sorted array must be the root of BST.
At the same time, the root of any child subtree must the middle number of part array. So I can use a recursion function to solve it.

```
public class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {
        if(nums.length==0) return null;  
        return helper(nums,0,nums.length-1);
    }
    
    public TreeNode helper(int[] nums, int start, int end){
        if(end-start<0) return null;
        int middle = (start+end)/2;
        TreeNode root = new TreeNode(nums[middle]);     
        
        root.left = helper(nums,start,middle-1);
        root.right = helper(nums,middle+1,end);
        return root;
    }
}
```
