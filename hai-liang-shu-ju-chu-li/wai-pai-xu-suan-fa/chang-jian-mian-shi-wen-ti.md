# 常见面试问题

### 合并k个排序文件:

* 这个就是很直白的外排序的应用, 直接在内存里面开个heap, 然后输出即可

### 求两个超大文件的交际:

* 这个题目我们可以分情况讨论:
  * 在这些url中没有重复的
    * 通常的解决方案都是把大文件按照hash function拆成小文件, 理想情况下, 这个hash的分布是均匀的, 那么这些小文件的大小也就是一致的. 然后先把一个文件load到内存里, 另一个也load到内存里逐个比较即可\(或者直接使用set的交集function\)
    * 不理想的情况, hash可能导致某些文件的hash很集中, 怎么解决?
      * 方法一: 在这种情况下, 我们需要换一个hash function再次进行拆分
      * 方法二: 使用Bloom filter, 开一个很大的数组, 缺点是如果内存大小不大于\(\)其中一个文件的大小 \* hash function的数量 \* 10\), 那么会出现很多的false positive, 那么这时候我们还是需要文件拆分
      * 方法三: 使用外排序, 把文件分成文件大小/内存大小的个数, 然后进行外排序, 如果有重复的就记录下来, 没重复的就跳过即可
  * 在这些url中有重复的
    * 有重复的情况, hash function有可能导致某些小文件拥有大量的url, 举一个最坏的例子, 如这些url全部都是一样的, 那么hash和不hash其实是没有任何区别的. 在这种情况下, 我们可以先去重, 然后在使用hash function拆分即可
    * 要注意这里的外排序不需要对两个文件单独去重
    * 使用bloom filter也不需要先去重, 反正标记的是有没有

