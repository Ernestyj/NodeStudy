



title: Remove Duplicates from Sorted Array II - 从有序数组中移除重复元素II
date: 2016-01-01 20:44:47
categories: 
- 算法
tags: 
- java
- 算法
- LeetCode
<!--updated: 2016-01-01 21:40:47-->
---

### Remove Duplicates from Sorted Array II - 从有序数组中移除重复元素II

**Description**: Follow up for "Remove Duplicates": What if duplicates are allowed at most twice?

 Note: Do not allocate extra space for another array, you must do this in place with constant memory.
 
 For example,
 Given sorted array nums = [1,1,1,2,2,3],
 Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3. It doesn't matter what you leave beyond the new length.
 
今天是2016.1.1元旦节，新年快乐！
![2016](/images/2016.png)

思路：与Remove Duplicates from Sorted Array一致，用index存不同数字的个数(可以含两次重复的数字)，遍历数组判断当前值是否和前一个值不一样。如果不一样，就是一个新的值，更新数组并对index加1。

完整的java代码如下：

```java
public class RemoveDuplicatesFromSortedArrayII {


    public static void main(String[] args) {
        int[] nums = {-2, -1, 0, 0, 1, 2, 2, 4, 6};
//        int[] nums = {1};
        System.out.println("************************");
        int count = new RemoveDuplicatesFromSortedArrayII().removeDuplicates(nums);
        System.out.println(count);
        for (int i : nums) System.out.print(i + " ");
    }


    /**
     * 用index存不同数字的个数(可以含两次重复的数字)，遍历数组判断当前值是否和前一个值不一样。
     如果不一样，就是一个新的值，更新数组并对index加1。
     * @param nums
     * @return
     */
    public int removeDuplicates(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        int index = 1;
        int count = 0;
        for (int i=1; i<nums.length; i++){
            if (nums[i] != nums[i-1]){
                nums[index++] = nums[i];    //其实 index++; 即可
                count = 0;
            } else {
                count++;
                if (count < 2){
                    nums[index++] = nums[i];    //其实 index++; 即可
                }
            }
        }
        return index;
    }

}
```
