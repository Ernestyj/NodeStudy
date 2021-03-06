




title: Clone Graph - 复制无向图
date: 2016-02-21 20:44:47
categories: 
- 算法
tags: 
- java
- 算法
- LeetCode
<!--updated: 2016-02-21 21:40:47-->
---

### Clone Graph - 复制无向图
**Description**: Clone an undirected graph. Each node in the graph contains a label and a list of its neighbors.

原题参见：https://leetcode.com/problems/clone-graph/
 
思路：无向图深拷贝,BFS，用到一个队列和旧节点到新节点的映射。

完整的java代码如下：

```java
public class CloneGraph {

    class UndirectedGraphNode {
        int label;
        List<UndirectedGraphNode> neighbors;
        UndirectedGraphNode(int x) { label = x; neighbors = new ArrayList<UndirectedGraphNode>(); }
    }

    /**
     * 无向图深拷贝,BFS
     * @param node
     * @return
     */
    public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
        if(node == null) return null;
        LinkedList<UndirectedGraphNode> queue = new LinkedList<>();
        HashMap<UndirectedGraphNode, UndirectedGraphNode> map = new HashMap<>();
        UndirectedGraphNode newHead = new UndirectedGraphNode(node.label);
        queue.offer(node);
        map.put(node, newHead);
        while(!queue.isEmpty()){
            UndirectedGraphNode curr = queue.poll();
            for(UndirectedGraphNode aNeighbor: curr.neighbors){
                if(!map.containsKey(aNeighbor)){
                    UndirectedGraphNode copy = new UndirectedGraphNode(aNeighbor.label);
                    map.put(aNeighbor, copy);
                    map.get(curr).neighbors.add(copy);
                    queue.add(aNeighbor);
                }else{
                    map.get(curr).neighbors.add(map.get(aNeighbor));
                }
            }
        }
        return newHead;
    }

    //无向图深拷贝,BFS,比上面的方法慢
    public UndirectedGraphNode cloneGraph1(UndirectedGraphNode node) {
        if (node==null) return null;
        Queue<UndirectedGraphNode> queue = new LinkedList<>();
        Queue<UndirectedGraphNode> originQueue = new LinkedList<>();
        Map<Integer, UndirectedGraphNode> map = new HashMap<>();
        queue.offer(node);
        originQueue.offer(node);
        map.put(node.label, new UndirectedGraphNode(node.label));
        while (!queue.isEmpty()) {
            UndirectedGraphNode theNode = queue.poll();
            for (UndirectedGraphNode n : theNode.neighbors){
                if (!map.containsKey(n.label)){
                    map.put(n.label, new UndirectedGraphNode(n.label));
                    queue.offer(n);
                    originQueue.offer(n);
                }
            }
        }
        while (!originQueue.isEmpty()) {
            UndirectedGraphNode theNode = originQueue.poll();
            UndirectedGraphNode newNode = map.get(theNode.label);
            for (UndirectedGraphNode n : theNode.neighbors){
                newNode.neighbors.add(map.get(n.label));
            }
        }
        return map.get(node.label);
    }

}
```
