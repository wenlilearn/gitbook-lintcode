# 在线算法

在线算法其实和离线算法很像, 不过这里没有办法一次性知道所有单词的出现概率, 这个时候我们还是通过hashmap和heap, 只不过我们要动态的调整heap, 下面这个题目就是与这个有关的

{% tabs %}
{% tab title="Problem" %}

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

