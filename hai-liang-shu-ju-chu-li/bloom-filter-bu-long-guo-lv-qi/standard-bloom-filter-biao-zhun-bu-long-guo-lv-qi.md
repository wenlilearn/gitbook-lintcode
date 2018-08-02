# Standard bloom filter\(标准布隆过滤器\)

### 标准布隆过滤器:

* 标准布隆过滤器是使用n个哈希函数和一个大数组来检测元素是不是在一个集合中
* 用来代替hashset
* 题目如下

{% tabs %}
{% tab title="Problem" %}
#### 556. Standard Bloom Filter

Implement a standard bloom filter. Support the following method:

1. `StandardBloomFilter(k)`,The constructor and you need to create k hash functions.
2. `add(string)`. add a string into bloom filter.
3. `contains(string)`. Check a string whether exists in bloom filter.

#### Example

```text
StandardBloomFilter(3)
add("lint")
add("code")
contains("lint") // return true
contains("world") // return false
```

Input test data \(one parameter per line.\)  
{% endtab %}

{% tab title="Java" %}
```java
import java.util.BitSet;

class HashFunction {
    int cap, seed;
    
    public HashFunction(int cap, int seed){
        this.cap = cap;
        this.seed = seed;
    }
    
    public int hash(String word){
        int ret = 0;
        for(int i = 0; i < word.length(); i++){
            ret += ret * seed + word.charAt(i);
            ret %= cap;
        }
        
        return ret;
    }
}

public class StandardBloomFilter {
    /*
    * @param k: An integer
    */
    List<HashFunction> hashfunctions;
    BitSet bits;
    int k;
    
    public StandardBloomFilter(int k) {
        // do intialization if necessary
        this.k = k;
        hashfunctions = new ArrayList<HashFunction>();
        for(int i = 0; i < k; i++){
            hashfunctions.add(new HashFunction(100000 + i, 2 * i + 3));
        }
        bits = new BitSet(100000 + k);
    }

    /*
     * @param word: A string
     * @return: nothing
     */
    public void add(String word) {
        // write your code here
        for(int i = 0; i < k; i++){
            int pos = hashfunctions.get(i).hash(word);
            bits.set(pos);
        }
    }

    /*
     * @param word: A string
     * @return: True if contains word
     */
    public boolean contains(String word) {
        // write your code here
        for(int i = 0; i < k; i++){
            int pos = hashfunctions.get(i).hash(word);
            if(!bits.get(pos)){
                return false;
            }
        }
        
        return true;
    }
}
```
{% endtab %}
{% endtabs %}

