




title: Rotate Array - 旋转数组
date: 2016-03-26 20:44:47
categories: 
- 算法
tags: 
- java
- 算法
- LeetCode
<!--updated: 2016-03-26 21:40:47-->
---

### Rotate Array - 旋转数组
**Description**: Rotate an array of n elements to the right by k steps.
 For example, with n = 7 and k = 3, the array [1,2,3,4,5,6,7] is rotated to [5,6,7,1,2,3,4].
 Note: Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.
 Hint: Could you do it in-place with O(1) extra space?

思路：一、O(1) space and in O(n) time.
Assuming we are given {1,2,3,4,5,6} and order 2. The basic idea is:
     1. Divide the array two parts: 1,2,3,4 and 5, 6
     2. Rotate first part: 4,3,2,1,5,6
     3. Rotate second part: 4,3,2,1,6,5
     4. Rotate the whole array: 5,6,1,2,3,4
  二、数组复制
  三、冒泡法
     
参考链接：http://www.programcreek.com/2015/03/rotate-array-in-java/

完整的java代码如下（法一）：

```java
public class RotateArray {

    /**
     * O(1) space and in O(n) time.
     Assuming we are given {1,2,3,4,5,6} and order 2. The basic idea is:
     1. Divide the array two parts: 1,2,3,4 and 5, 6
     2. Rotate first part: 4,3,2,1,5,6
     3. Rotate second part: 4,3,2,1,6,5
     4. Rotate the whole array: 5,6,1,2,3,4
     http://www.programcreek.com/2015/03/rotate-array-in-java/
     * @param nums
     * @param k
     */
    public void rotate(int[] nums, int k) {
        k = k%nums.length;
        if (k==0) return;
        reverse(nums, 0, nums.length-k);
        reverse(nums, nums.length-k, nums.length);
        reverse(nums, 0, nums.length);
    }
    private void reverse(int[] nums, int start, int end){
        int l = start+end;
        for (int i=start; i<l/2; i++){
            int temp = nums[i];
            nums[i] = nums[l-i-1];
            nums[l-i-1] = temp;
        }
    }

}
```
