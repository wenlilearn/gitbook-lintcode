# Untitled

{% tabs %}
{% tab title="Problem" %}
#### 430. Flatten a Multilevel Doubly Linked List

You are given a doubly linked list which in addition to the next and previous pointers, it could have a child pointer, which may or may not point to a separate doubly linked list. These child lists may have one or more children of their own, and so on, to produce a multilevel data structure, as shown in the example below.

Flatten the list so that all the nodes appear in a single-level, doubly linked list. You are given the head of the first level of the list.

**Example:**

```text
Input:
 1---2---3---4---5---6--NULL
         |
         7---8---9---10--NULL
             |
             11--12--NULL

Output:
1-2-3-7-8-11-12-9-10-4-5-6-NULL
```
{% endtab %}

{% tab title="Solution" %}
### Recursion:

* 如果碰到叶节点\(没有child也没有next\)直接返回
* 如果碰到的节点有child:
  * 递归的去flatten这个child
  * 这个递归会返回被flatten以后的链表的tail
  * 把原来链表的next设为child的
  * 把child的prev设为原来节点
  * 把返回的tail的next设为next
  * 把原来的next的prev设为tail\(如果有的话\)
  * 把child设为null
  * 然后递归的去call flatten\(cur.next\)
{% endtab %}

{% tab title="Java" %}
```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node prev;
    public Node next;
    public Node child;

    public Node() {}

    public Node(int _val,Node _prev,Node _next,Node _child) {
        val = _val;
        prev = _prev;
        next = _next;
        child = _child;
    }
};
*/
class Solution {
    public Node flatten(Node head) {    
      if(head == null){
        return head;
      }
      dfs(head);
      
      return head;
    }
  
    private Node dfs(Node head) {
      if(head == null || head.child == null && head.next == null){
        return head;
      }
      
      if(head.child != null){
        Node child = head.child;
        Node next = head.next;
        Node flatHead = dfs(head.child);
        
        flatHead.next = next;
        if(next != null){
          next.prev = flatHead;
        }
        head.next = child;
        child.prev = head;
        head.child = null;
      }
      
      return dfs(head.next);
    }
}
```
{% endtab %}
{% endtabs %}

