# 18. Subsets II

{% tabs %}
{% tab title="Problem" %}
#### 18. Subsets II

Given a collection of integers that might contain duplicates, _nums_, return all possible subsets \(the power set\).

#### Example

Input: `[1,2,2]`  
Output:

```text
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```

#### Challenge

Can you do it in both recursively and iteratively8. Subsets II
{% endtab %}

{% tab title="Solution" %}
### DFS\(组合类\):

* 这个题目和subsets I是类似问题, 无非多出来了重复元素
* 对于重复元素的办法是
  * 先把数组排序
  * 碰到i &gt; start && \[i\] == \[i - 1\]就continue即可
{% endtab %}

{% tab title="Java" %}
```java
public class Solution {
    /**
     * @param nums: A set of numbers
     * @return: A list of lists
     */
    List<Integer> local = new ArrayList<>();
    List<List<Integer>> res = new ArrayList<>();
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        // write your code here
        if(nums == null || nums.length == 0){
          res.add(local);
          
          return res;
        }
        
        Arrays.sort(nums);
        
        dfs(nums, 0);
        
        return res;
    }
    
    private void dfs(int[] nums, int start){
      if(start > nums.length){
        return;
      }
      
      res.add(new ArrayList<Integer>(local));
      
      for(int i = start; i < nums.length; i++){
        if(i > start && nums[i] == nums[i - 1]){
          continue;
        }
        
        local.add(nums[i]);
        dfs(nums, i +  1);
        local.remove(local.size() - 1);
      }
    }
}
```
{% endtab %}
{% endtabs %}



