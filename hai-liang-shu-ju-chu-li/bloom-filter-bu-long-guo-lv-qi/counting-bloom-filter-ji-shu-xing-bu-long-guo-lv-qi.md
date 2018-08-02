# Counting bloom filter\(计数型布隆过滤器\)

### 计数型布隆过滤器:

* 计数型布隆过滤器主要是通过记录元素经过每个hash function以后所在的index在数组中出现的次数
* 当查找元素的时候, 我们分别使用hash function找到对应的index, 然后找到所有数组对应index值中的最小的那个
* 用来代替hashmap
* 题目如下:

{% tabs %}
{% tab title="Problem" %}
#### 555. Counting Bloom Filter

Implement a counting bloom filter. Support the following method:

1. `add(string)`. Add a string into bloom filter.
2. `contains(string)`. Check a string whether exists in bloom filter.
3. `remove(string)`. Remove a string from bloom filter.

#### Example

```text
CountingBloomFilter(3) 
add("lint")
add("code")
contains("lint") // return true
remove("lint")
contains("lint") // return false
```
{% endtab %}

{% tab title="Java" %}
```java
class HashFunction{
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

public class CountingBloomFilter {
    /*
    * @param k: An integer
    */
    private int k;
    private List<HashFunction> hfs;
    private int[] bits;
    
    public CountingBloomFilter(int k) {
        // do intialization if necessary
        this.k = k;
        this.hfs = new ArrayList<HashFunction>();
        for(int i = 0; i < k; i++){
            hfs.add(new HashFunction(100000 + i, 2 * i + 3));
        }
        
        //这里把bitset换成了int, 因为要数元素出现的个数
        bits = new int[100000 + k];
    }

    /*
     * @param word: A string
     * @return: nothing
     */
    public void add(String word) {
        // write your code here
        for(int i = 0; i < k; i++){
            int pos = hfs.get(i).hash(word);
            bits[pos] += 1;
        }
    }

    /*
     * @param word: A string
     * @return: nothing
     */
    public void remove(String word) {
        // write your code here
        for(int i = 0; i < k; i++){
            int pos = hfs.get(i).hash(word);
            bits[pos] -= 1;
        }
    }

    /*
     * @param word: A string
     * @return: True if contains word
     */
    public boolean contains(String word) {
        // write your code here
        for(int i = 0; i < k; i++){
            int pos = hfs.get(i).hash(word);
            
            if(bits[pos] <= 0){
                return false;
            }
        }
        return true;
    }
}
```
{% endtab %}
{% endtabs %}

