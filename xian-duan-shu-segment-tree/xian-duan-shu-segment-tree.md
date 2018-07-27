# 201. Segment Tree Build

{% tabs %}
{% tab title="Problem" %}
#### 201. Segment Tree Build

The structure of Segment Tree is a binary tree which each node has two attributes `start` and `end` denote an segment / interval.

_start_ and _end_ are both integers, they should be assigned in following rules:

* The root's _start_ and _end_ is given by `build` method.
* The left child of node A has `start=A.left, end=(A.left + A.right) / 2`.
* The right child of node A has `start=(A.left + A.right) / 2 + 1, end=A.right`.
* if _start_ equals to _end_, there will be no children for this node.

Implement a `build` method with two parameters _start_ and _end_, so that we can create a corresponding segment tree with every node has the correct _start_ and _end_ value, return the root of this segment tree.

#### Example

Given `start=0, end=3`. The segment tree will be:

```text
               [0,  3]
             /        \
      [0,  1]           [2, 3]
      /     \           /     \
   [0, 0]  [1, 1]     [2, 2]  [3, 3]
```

Given `start=1, end=6`. The segment tree will be:

```text
               [1,  6]
             /        \
      [1,  3]           [4,  6]
      /     \           /     \
   [1, 2]  [3,3]     [4, 5]   [6,6]
   /    \           /     \
[1,1]   [2,2]     [4,4]   [5,5]
```

Input test data \(one parameter per line.\)  
{% endtab %}

{% tab title="Solution" %}
### Segment Tree:

* 线段树的构建
  * 把区间分成两半
  * 先建立左边一半, 再建立右边一半
  * 然后建立root
* 这个题目在线段树的node里面什么也不用存, 所以直接连上左右两颗子树返回即可
{% endtab %}

{% tab title="Java" %}
```java
/**
 * Definition of SegmentTreeNode:
 * public class SegmentTreeNode {
 *     public int start, end;
 *     public SegmentTreeNode left, right;
 *     public SegmentTreeNode(int start, int end) {
 *         this.start = start, this.end = end;
 *         this.left = this.right = null;
 *     }
 * }
 */


public class Solution {
    /*
     * @param start: start value.
     * @param end: end value.
     * @return: The root of Segment Tree.
     */
    public SegmentTreeNode build(int start, int end) {
        // write your code here
        if(start > end){
          return null;
        }
        
        if(start == end){
          return new SegmentTreeNode(start, end);
        }
        
        int mid = (start + end) / 2;
        SegmentTreeNode left = build(start, mid);
        SegmentTreeNode right = build(mid + 1, end);
        
        SegmentTreeNode root = new SegmentTreeNode(start, end);
        root.left = left;
        root.right = right;
        
        return root;
    }
}
```
{% endtab %}
{% endtabs %}

