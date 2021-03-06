



title: Search for a Range
date: 2015-11-17 20:44:47
categories: 
- 算法
tags: 
- java
- 算法
- LeetCode
<!--updated: 2015-11-17 21:40:47-->
---

### Search for a Range

**Description**: Given a sorted array of integers, find the starting and ending position of a given target value.
 Your algorithm's runtime complexity must be in the order of O(log n).
 If the target is not found in the array, return [-1, -1].

 For example,
 Given [5, 7, 7, 8, 8, 10] and target value 8,
 return [3, 4].

完整的java代码如下：

```java
public class SearchForARange {

    public static void main(String[] args) {

        int[] nums = {5, 7, 7, 8, 8, 10};
        int[] range = new SearchForARange().searchRange(nums, 7);

        System.out.println("*****RESULT*****");
        System.out.println(range[0] + ", " + range[1]);
    }


    public int[] searchRange(int[] nums, int target) {
        int[] range = {-1, -1};
        if (nums == null || nums.length == 0) return range;
        int l = 0, r = nums.length - 1;
        int m = 0;
        while (l <= r){
            m = (l + r) / 2;
            if (target < nums[m]) r = m - 1;
            else if (nums[m] < target) l = m + 1;
            else {
                for (int i = m; i <= r; i++){
                    if (nums[i] == target) range[1] = i;
                    else break;
                }
                for (int j = m; j >= l; j--){
                    if (nums[j] == target) range[0] = j;
                    else break;
                }
                return range;
            }
        }
        return range;
    }


}
```
