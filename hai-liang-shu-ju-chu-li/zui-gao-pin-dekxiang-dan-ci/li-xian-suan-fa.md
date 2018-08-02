# 离线算法



离线算法就是统计所有单词出现的概率, 然后根据出现次数进行排序

* 哈希表+最小堆即可实现
* 或者是用最小堆放入前面k个单词, 然后依次淘汰出现次数最小的那个

Followup: 能不能更快?

* 单机的话应该是没有办法了
* 如果有多台机器的话, 可以使用Map Reduce:
  * Map Reduce是一个通用的解决分布式计算问题的框架
  * 如果使用Map Reduce的话, 一共分为三个步骤:
    * Map: 对每一个mapper的文件进行处理, 统计出单词在这个文件中的出现此处, 记为&lt;word, 1&gt;
    * Reduce: 每一个reducer被预先分配了要处理的单词, 收到数据以后, 就会将要处理的单词的key进行整合, 然后每个reducer输出他所见到的前k高频的单词
    * 最后通过这些reducer输出结果返回top k个单词即可
* 为什么不能通过把一个大文件拆成n个小文件, 然后每个文件都返回前k个单词? 因为这样有可能导致单词统计的概率不正确

Followup: 如何解决内存不足的问题?

* 假设给定的内存空间没有办法存储所有的单次出现的频率, 这时候应该怎么办?
* 我们可以通过哈希函数把单词变成整数, 这样就能极大地降低空间使用
* 具体实现差不多就是:
  * 扫描大文件, 建立哈希表, key是单词经过哈希函数的输出, value是0
  * 把大文件先分割成小文件\(~磁盘 \* 2/内存\)
  * 然后对于每个文件进行统计, 统计单词和出现频率
    * 与此同时不断的淘汰最小堆
