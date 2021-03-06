




title: Contains Duplicate III - 重复元素III
date: 2016-04-14 20:44:47
categories: 
- 算法
tags: 
- java
- 算法
- LeetCode
<!--updated: 2016-04-14 21:40:47-->
---

### Contains Duplicate III - 重复元素III
**Description**: Given an array of integers, find out whether there are two distinct indices i and j in the array such that the difference between nums[i] and nums[j] is at most t and the difference between i and j is at most k.
 
思路：O(nlog(k)),借助TreeSet维护窗口k

参考链接：http://www.programcreek.com/2014/06/leetcode-contains-duplicate-iii-java/

完整的java代码如下：

```java
public class ContainsDuplicateIII {

    /**
     * O(nlog(k)),借助TreeSet维护窗口k
     * http://www.programcreek.com/2014/06/leetcode-contains-duplicate-iii-java/
     * @param nums
     * @param k
     * @param t
     * @return
     */
    public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
        if (k < 1 || t < 0) return false;
        TreeSet<Integer> set = new TreeSet<>();
        for (int i=0; i<nums.length; i++) {
            int c = nums[i];
            if ((set.floor(c)!=null && c<=set.floor(c)+t)
                    || (set.ceiling(c)!=null && c>=set.ceiling(c)-t))
                return true;
            set.add(c);
            if (i>=k) set.remove(nums[i-k]);
        }
        return false;
    }

    //(此法超时)维护窗口k, 注意边界情况 [-1,2147483647] 1 2147483647
    public boolean containsNearbyAlmostDuplicate1(int[] nums, int k, int t) {
        if (nums==null || nums.length<=1) return false;
        int i, j;
        int len;
        if (nums.length-1<=k) len = nums.length-1;
        else len = k;
        for (i=0; i<=len; i++){
            for (j=i+1; j<=len; j++){
                if (i!=j && Math.abs((long)nums[j]-nums[i])<=t) return true;
            }
        }
        if (nums.length-1<=k) return false;
        for (i=k+1; i<nums.length; i++){    //窗口滚动
            for (j=i-k; j<i; j++){
                if (Math.abs((long)nums[j]-nums[i])<=t) return true;
            }
        }
        return false;
    }

}
```
