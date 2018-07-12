# Rabin-Karp

{% tabs %}
{% tab title="Solution" %}
### Rabin-Karp:

* Rabin-Karp算法是KMP算法的替代品, 也是希望在O\(m + n\)的时间内解决在字符串中寻找子串这种问题
* 方法就是:
  * 先把新的字母加入要被hash的字符串中
  * 不断地对字符串进行hash
  * 同时比较source的hash和target的hash
  * 如果两个hash相同
    * 那么需要比较两个字符串
  * 如果不相等, 有点像sliding window, 去掉最前面见过的字符
{% endtab %}

{% tab title="Java" %}
```java
public class Solution {
    /*
     * @param source: A source string
     * @param target: A target string
     * @return: An integer as index
     */
    // Base for mod operation
    private static final int BASE = 100000;
    public int strStr2(String source, String target) {
        // write your code here
        if(source == null || target == null){
          return -1;
        }
        
        if(target.equals("")){
          return 0;
        }
        
        int m = target.length();
        // power stores 31^m, used to substract out of hash
        // 这里计算最高的power也是用target的长度
        int power = 1;
        for(int i = 0; i < m; i++){
          power = (power * 31) % BASE;
        }
        
        // target_hash stores the hash for target string
        // used for comparsion later to source_hash
        int target_hash = 0;
        for(int i = 0; i < m; i++){
          target_hash = (target_hash * 31 + (int)target.charAt(i)) % BASE;
        }
        
        // start calculating source_hash
        int source_hash = 0;
        // 就这里我们遍历source, 所以用source的长度进行遍历
        for(int i = 0; i < source.length(); i++){
          source_hash = (source_hash * 31 + (int)source.charAt(i)) % BASE;
          // If we haven't seen enough characters, we don't need to compare
          // hash. Just pass through
          // 这之后都应该是用target
          if(i < m - 1){
            continue;
          }
          
          // If we have seen more than m character, we need to take the 
          // first one out. The first one is the one at i - m
          if(i >= m){
            source_hash = source_hash - (power * source.charAt(i - m)) % BASE;
            // Due to the fact that mod is not right
            if(source_hash < 0){
              source_hash += BASE;
            }
          }
          
          // Same hash. Need to compare the two strings
          // Starting index for the current string is i - m + 1
          if(source_hash == target_hash){
            String sub_source = source.substring(i - m + 1, i + 1);
            
            if(sub_source.equals(target)){
              return i - m + 1;
            }
          }
        }
        
        return -1;
    }
}
```
{% endtab %}
{% endtabs %}

