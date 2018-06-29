# Partition vs Quick Sort\(Select\)



### Partition:

* 一定要把一个数组严格的分成两个部分
* 一般来说是左边&lt;=, 右边&gt;

### Quick Sort\(Select\):

* 不严格的把数组分成两个部分, 中间的元素有可能混合在两边之中
* 但是最后一定会保证中间的元素在中间
* 一般来说左边&lt;, 右边&gt;

#### Quick Sort vs Quick Select

* QuickSort:
  * 有两个recursive call, 分别对应了两边, 因为要保证两边都有顺序
  * 当start==end的时候, 直接return
  * 函数没有返回值
* QuickSelect
  * 只会选择一边进行recursive call
  * 当start==end的时候, return \[start\]
  * 函数有返回值, 返回的就是第k个元素

