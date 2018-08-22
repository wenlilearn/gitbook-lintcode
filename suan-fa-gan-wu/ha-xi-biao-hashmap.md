# 哈希表\(HashMap\)

### 原理:

* 实现是&lt;key, value&gt;, 就像一本字典的目录:
  * 给定一个单词
  * 能找到单词所在的页数\(通过hash function把单词转化成页数\)
  * 然后在这一页里面能找到单词和单词的定义\(一般两个都存在一起\)
* 有collision, 有两种解决方式:
  * open hash: 使用链表解决哈希冲突
  * close hash: 通过找下一个空余位置来解决哈希
* 哈希函数:

  * 目的是为了把一个key转化为一个整数, 而且这个整数是固定而且没有规律的
  * 一般来说, 我们选择使用如下的hash function实现:

  ```text
  keys = [...]
  hash = 0
  hash_size = <An arbitrary hash size>

  for key in keys:
      hash = ((hash) * <large prime> + key) % hash_size
  ```

* Rehash:
  * 当哈希表里面的元素跟哈希表的空间的比例约为1:20/50的时候, 那么就开始rehash
  * 基本的过程就是对于所有hash table里面的元素, 重新用hash function算出hash, 然后放入相应的位置
  * 空间比例可以调整, 一般来说, 调整的时候占比越小, 哈希表的效率越高, 但是空间占用也就越大

