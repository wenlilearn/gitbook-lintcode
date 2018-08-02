# 在线算法

在线算法其实和离线算法很像, 不过这里没有办法一次性知道所有单词的出现概率, 这个时候我们还是通过hashmap和heap, 只不过我们要动态的调整heap, 下面这个题目就是与这个有关的

{% tabs %}
{% tab title="Problem" %}
#### 550. Top K Frequent Words II

Find top _k_ frequent words in realtime data stream.

Implement three methods for _Topk_ Class:

1. `TopK(k)`. The constructor.
2. `add(word)`. Add a new word.
3. `topk()`. Get the current top _k_ frequent words.

#### Example

```text
TopK(2)
add("lint")
add("code")
add("code")
topk()
>> ["code", "lint"]
```
{% endtab %}

{% tab title="Java" %}
```java
public class TopK {
    Map<String, Integer> freq;
    TreeSet<String> min_heap;
    int k;
    
    class WordComparator implements Comparator<String> {
      public int compare(String left, String right){
        int left_count = freq.get(left);
        int right_count = freq.get(right);
        if (left_count != right_count) {
            return right_count - left_count;
        }
        return left.compareTo(right);
      }
    }
    /*
    * @param k: An integer
    */public TopK(int k) {
        // do intialization if necessary
        freq = new HashMap<String, Integer>();
        min_heap = new TreeSet<String>(new WordComparator());
        this.k = k;
    }

    /*
     * @param word: A string
     * @return: nothing
     */
    public void add(String word) {
        // write your code here
        if(!freq.containsKey(word)){
          freq.put(word, 1);
        } else {
        //这里必须先处理heap, 不然改变了word的freq再处理heap会导致
        //heap的位置发生错乱
          if(min_heap.contains(word)){
            min_heap.remove(word);
          }
          freq.put(word, freq.get(word) + 1);
        }
        
        min_heap.add(word);

        if(min_heap.size() > k){
          min_heap.pollLast();
        }
    }

    /*
     * @return: the current top k frequent words.
     */
    public List<String> topk() {
        // Write your code here
        List<String> results = new ArrayList<String>();
        Iterator it = min_heap.iterator();
        //treeset可以用iterator, 很神奇
        while(it.hasNext()) {
             String str = (String)it.next();
             results.add(str);
        }
        return results;
    }
}
```
{% endtab %}
{% endtabs %}

### Followup: 内存不足怎么办?

* 首先来说, 一个精确的, 在线的, 省空间的算法在内存不足的情况下是不存在的
* 但是我们可以通过某些estimate的算法, 在这里我们选择hashcount
* hashcount的原理就是把word用hash function进行hash, 然后用这个hash来代替word
* hash function虽然会有collision, 不过这样正好使得我们减小了空间的占用
* 伪代码如下:

```java
hash_map = new int[hash_size];
hash_code = hash_function(word) % hash_size
hash_map[hash_code] += 1
```

