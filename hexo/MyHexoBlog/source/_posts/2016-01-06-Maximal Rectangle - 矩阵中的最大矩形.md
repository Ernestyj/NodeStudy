



title: Maximal Rectangle - 矩阵中的最大矩形
date: 2016-01-06 20:44:47
categories: 
- 算法
tags: 
- java
- 算法
- LeetCode
<!--updated: 2016-01-06 21:40:47-->
---

### Maximal Rectangle - 矩阵中的最大矩形

**Description**: Given a 2D binary matrix filled with 0's and 1's, find the largest rectangle containing all ones and return its area.
 

思路：http://www.cnblogs.com/lichen782/p/leetcode_maximal_rectangle.html 中给出了O(n^3)的普通方法（但会大数据超时）。高效的方法：转化为Largest Rectangle in Histogram的问题，时间复杂为O(n^2).

完整的java代码如下：

```java
public class MaximalRectangle {

    public static void main(String[] args) {
        System.out.println("*****RESULT*****");
    }

    /**
     * http://www.cnblogs.com/lichen782/p/leetcode_maximal_rectangle.html 中给出了O(n^3)的普通方法（会大数据超时）。
     * 高效的方法：转化为Largest Rectangle in Histogram的问题，时间复杂为O(n^2).
     * @param matrix
     * @return
     */
    public int maximalRectangle(char[][] matrix) {
        if (matrix.length == 0) return 0;
        int m = matrix.length;
        int n = matrix[0].length;
        //实际上height可以分配一维数组存储
        int[][] height = new int[m][n + 1]; //末尾多加一个dummy元素0
        int maxArea = 0;
        //矩阵按行转化为柱状图
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (matrix[i][j] == '0') {
                    height[i][j] = 0;
                } else {
                    height[i][j] = (i == 0) ? 1 : height[i - 1][j] + 1;
                }
            }
        }
        //计算每个柱状图的最大矩形面积
        for (int i = 0; i < m; i++) {
            int area = maxAreaInHist(height[i]);
            if (area > maxArea) {
                maxArea = area;
            }
        }
        return maxArea;
    }
    //Largest Rectangle in Histogram算法，传入的height数组最后一个元素是多加的dummy元素
    private int maxAreaInHist(int[] height) {
        Stack<Integer> stack = new Stack<>();
        int i = 0;
        int maxArea = 0;
        while (i < height.length) {
            if (stack.isEmpty() || height[stack.peek()] <= height[i]) {
                stack.push(i++);
            } else {
                int t = stack.pop();
                maxArea = Math.max(maxArea, height[t] * (stack.isEmpty() ? i : i - stack.peek() - 1));
            }
        }
        return maxArea;
    }

}
```
