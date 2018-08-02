# Bloom Filter\(布隆过滤器\)

### 布隆过滤器:

* 有一个很大的数组和n个hash function组成
  * 对于给定的任何一个元素, 通过这n个hash function会产生n个整数
  * 把这n个整数取数组长度的模
  * 然后把数组中n % size这一项设成1
* 一般来说, 布隆过滤器用于解决以下的两种问题:
  * 查看一个元素在不在一个集合中
  * 统计元素出现的次数
* 如果这么看的话, 其实bloom filter和hashmap很像, 那么为什么使用bloom filter?
  * 因为bloom filter使用的空间比hashmap更小
* 那么bloom filter相对于hashmap有什么缺点?
  * bloom filter存在false positive, 如果一个元素出现在bloom filter里面, 那么它可能在这个集合里, 也有可能不在
  * 但如果一个元素不在bloom filter里面, 那么它一定不在集合里
* 两种bloom filter:
  * standard bloom filter: 用来处理元素在不在集合中这个问题, 对应hashset
  * counting bloom filter: 用来处理元素在集合中的出现次数, 对应hashmap
* 一般这个较大的数组开多大?
  * 一般为哈希函数个数 \* 10 \* 元素个数比较合适



