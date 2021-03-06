



title: Merge Intervals - 区间合并
date: 2015-12-09 20:44:47
categories: 
- 算法
tags: 
- java
- 算法
- LeetCode
<!--updated: 2015-12-09 21:40:47-->
---

### Merge Intervals - 区间合并

**Description**: Given a collection of intervals, merge all overlapping intervals.

 For example,
 Given [1,3],[2,6],[8,10],[15,18],
 return [1,6],[8,10],[15,18].
 
注意：输入集合不一定是按区间首部排序的。

思路：先按区间首部排序，再合并区间。

完整的java代码如下：

```java
public class MergeIntervals {

    public static void main(String[] args) {
        List<Interval> intervals = new ArrayList<>();
//        intervals.add(new Interval(1, 3));
//        intervals.add(new Interval(2, 6));
//        intervals.add(new Interval(8, 10));
//        intervals.add(new Interval(15, 18));
        intervals.add(new Interval(1,4));
        intervals.add(new Interval(0,4));
        System.out.println("*****RESULT*****");
        List<Interval> result = new MergeIntervals().merge(intervals);
        for (Interval interval : result){
            System.out.print("[" + interval.start + "," + interval.end + "] ");
        }
    }


    public static class Interval {
        int start;
        int end;
        Interval() { start = 0; end = 0; }
        Interval(int s, int e) { start = s; end = e; }
    }


    public List<Interval> merge(List<Interval> intervals) {
        List<Interval> result = new ArrayList<>();
        if (intervals == null || intervals.size() == 0) return result;
        HashMap<Integer, Interval> map = new HashMap<>();
        for (Interval interval : intervals){
            if (!map.containsKey(interval.start)) map.put(interval.start, interval);
            else {
                Interval oldInterval = map.get(interval.start);
                if (oldInterval.end < interval.end){
                    map.replace(oldInterval.start, interval);
                }
            }
        }
        List<Integer> sortedIntegers = new ArrayList<Integer>(map.keySet());
        Collections.sort(sortedIntegers);

        Interval firstInterval = map.get(sortedIntegers.get(0));
        int start = firstInterval.start;
        int end = firstInterval.end;
        for (Integer i : sortedIntegers){
            Interval interval = map.get(i);
            if (interval.start > end){
                result.add(new Interval(start, end));
                start = interval.start;
                end = interval.end;
            } else {
                if (interval.end > end){
                    end = interval.end;
                }
            }
        }
        result.add(new Interval(start, end));
        return result;
    }

}
```
