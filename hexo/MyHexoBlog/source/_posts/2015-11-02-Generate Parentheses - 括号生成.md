


title: Generate Parentheses - 括号生成
date: 2015-11-02 20:44:47
categories: 
- 算法
tags: 
- java
- 算法
- LeetCode
<!--updated: 2015-11-02 21:40:47-->
---

### Generate Parentheses - 括号生成

**Description**: Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

 For example, given n = 3, a solution set is:
 "((()))", "(()())", "(())()", "()(())", "()()()"

思路：回溯法，其中剪枝条件1：左右括号数小于num；剪枝条件2：左括号数>=右括号数。

java代码如下：

```java
public class GenerateParentheses {

    public static void main(String[] args) {
        List<String> result = new GenerateParentheses().generateParenthesis(5);
        System.out.println("*****RESULT*****");
        for (String s : result) System.out.println(s);
    }

    private int num = 0;
    private StringBuilder builder = new StringBuilder();
    private List<String> list = new ArrayList<>();
    public List<String> generateParenthesis(int n) {
        num = n;
        backtrack(1, builder, 0);
        return list;
    }
    /**
     * 剪枝条件1，左右括号数小于num
     * 剪枝条件2，左括号数>=右括号数
     *
     * @param i
     * @param builder
     * @param rightCount
     */
    private void backtrack(int i, StringBuilder builder, int rightCount){
        if (i > num * 2){
            list.add(builder.toString());
        } else {
            for (int isTake = 0; isTake <= 1; isTake++){    //0:( 1:)
                char c = isTake == 0 ? '(' : ')';
                int tempRightCount = rightCount + isTake * 1;
                if (i - tempRightCount <= num &&    //剪枝条件1，左右括号数小于num
                        i - tempRightCount >= tempRightCount){  //剪枝条件2，左括号数>=右括号数
                    builder.append(c);
                    rightCount = tempRightCount;
                    backtrack(i + 1, builder, rightCount);
                    rightCount -= isTake * 1;
                    builder.deleteCharAt(builder.length() - 1);
                }
            }
        }

    }

}
```
