# [Next Permutation][title]

## Description

Implement **next permutation**, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be **in-place** and use only constant extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.

`1,2,3` → `1,3,2`
`3,2,1` → `1,2,3`
`1,1,5` → `1,5,1`

**Tags:** Array


## 思路

题意是
这道题让我们求下一个排列顺序，由题目中给的例子可以看出来，如果给定数组是降序，则说明是全排列的最后一种情况，则下一个排列就是最初始情况，可以参见之前的博客 Permutations。我们再来看下面一个例子，有如下的一个数组

1　　2　　7　　4　　3　　1

下一个排列为：

1　　3　　1　　2　　4　　7

那么是如何得到的呢，我们通过观察原数组可以发现，如果从末尾往前看，数字逐渐变大，到了2时才减小的，然后我们再从后往前找第一个比2大的数字，是3，那么我们交换2和3，再把此时3后面的所有数字转置一下即可，步骤如下：

1　　2　　7　　4　　3　　1

1　　2　　7　　4　　3　　1

1　　3　　7　　4　　2　　1

1　　3　　1　　2　　4　　7



```java
public void nextPermutation(int[] nums) {
    //find first decreasing digit
    int mark = -1;
    for (int i = nums.length - 1; i > 0; i--) {
        if (nums[i] > nums[i - 1]) {
            mark = i - 1;
            break;
        }
    }
 
    if (mark == -1) {
        reverse(nums, 0, nums.length - 1);
        return;
    }
 
    int idx = nums.length-1;
    for (int i = nums.length-1; i >= mark+1; i--) {
        if (nums[i] > nums[mark]) {
            idx = i;
            break;
        }
    }
 
    swap(nums, mark, idx);
 
    reverse(nums, mark + 1, nums.length - 1);
}
 
private void swap(int[] nums, int i, int j) {
    int t = nums[i];
    nums[i] = nums[j];
    nums[j] = t;
}
 
private void reverse(int[] nums, int i, int j) {
    while (i < j) {
        swap(nums, i, j);
        i++;
        j--;
    }
}
```


## 结语

如果你同我一样热爱数据结构、算法、LeetCode，可以关注我 GitHub 上的 LeetCode 题解：[awesome-java-leetcode][ajl]



[title]: https://leetcode.com/problems/next-permutation
[ajl]: https://github.com/Blankj/awesome-java-leetcode
