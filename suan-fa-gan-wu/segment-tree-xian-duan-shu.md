# Segment Tree\(线段树\)

{% tabs %}
{% tab title="线段树基础" %}
### 定义

* 线段树是一个二叉树, 通常用于解决区间的最值以及和的查询问题

### 性质

* 树的高度为O\(log\(n\)\)

### 节点定义

* 节点通常有五个fields:
  * start: 区间开始
  * end: 区间结束
  * left: 左树
  * right: 右树
  * value: 在这个区间中的值
{% endtab %}

{% tab title="线段树的建立" %}
### 线段树的构建:

* 时间复杂度为O\(n\)
* 空间复杂度为O\(n\)
* 线段树的构建和普通的二叉树有一定的类似之处:
  * 出口: 当start &gt; end, 直接返回空
  * 出口: 当start==end, 建立叶子节点
  * 把区间分成两半, 一边是\[start, mid\], 另一边是\[mid + 1, end\]
  * 然后分别把两个区间建立线段树
  * 最后把当前区间建立一个节点, 存的值为它的两个孩子返回值经过处理后的那个值\(求最大, 最小, 和\)
* 伪代码如下:

```java
Node {
    start, end;
    left, right;
    max;    
    
    Node(start, end, max)
}

//这里以求区间最大值为例
build(A[]){
    return dfs(0, A.length, - 1, A)
}

dfs(start, end, A[]){
    //出口
    if start > end: return null
    if start == end: return new Node(start, end, A[start])
    
    mid = (start + end) / 2
    
    //分别建立左右两颗线段树
    left = dfs(start, mid, A)
    right = dfs(mid + 1, end, A)
    
    //建立当前node
    max = Integer.MIN_VALUE
    root = new Node(start, end, max)
    if(left.max > node.max): node.max = left.max
    if(right.max > node.max): node.max = right.max
    
    root.left = left, root.right = right
    
    return root
}
```
{% endtab %}

{% tab title="线段树的查询" %}
### 查询操作:

* 线段树的查询是基于对给定的区间进行分割, 把给定的大区间拆分成选段树上已有的区间, 然后就直接能找到要找的值
* 每次拆分都是根据当前给定区间的start, end以及当前root的mid\(是\(start + end\) / 2\)进行比较
  * 如果start &lt;= mid, 那么我们就比较左区间
  * 如果end &gt; mid, 那么我们就比较右区间
  * 最后汇总两个结果即可
* 时间复杂度是O\(log\(n\)\)
* 思想上有点像divide and conquer
* 伪代码如下

```java
//root = SegmentTree.build(A)
query(start, end, root):
    //异常处理: 如果给定的区间不存在, 那么就直接返回一个
    //make sense的值, 不然这种情况会崩溃
    if root == null: return Integer.MIN_VALUE
    //当前查询的区间包含了整个线段树的区间, 那么这个区间就
    //不需要再拆分了, 直接返回区间值即可
    if start <= root.start && end >= root.end:
        return root.val
    
    //把当前区间分成两半, 为了确定给定的大区间落在当前root
    //的左边还是右边
    root_mid = (root.start + root.end) / 2
    val = Integer.MIN_VALUE
    
    //start和左边有重合, 继续去左边查询区间
    if(start <= root_mid):
        val = max(val, query(start, end, root.left))
    
    //end和右边有重合, 继续去右边查询区间
    if(end > root_mid):
        val = max(query(start, end, root.right))
    
    return val
```
{% endtab %}
{% endtabs %}

