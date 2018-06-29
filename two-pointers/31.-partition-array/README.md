# 31. Partition Array



{% tabs %}
{% tab title="Problem" %}
Given an array `nums` of integers and an int `k`, partition the array \(i.e move the elements in "nums"\) such that:

* All elements &lt; _k_ are moved to the _left_
* All elements &gt;= _k_ are moved to the _right_

Return the partitioning index, i.e the first index _i_ nums\[_i_\] &gt;= _k_.

#### Example

If nums = `[3,2,2,1]` and `k=2`, a valid answer is `1`.

#### Challenge

Can you partition the array in-place and in O\(n\)?Input test data \(one parameter per line.\)  
{% endtab %}

{% tab title="Solution" %}
#### Partition:

* 小于放左边, 大于等于放右边
* 注意这里的partition和quick sort里面的不太一样, 原因在于对于partition来说, 一定要把这个数组变成两个独立的部分, 左边一定是要&lt;=, 右边一定是要&gt;
* 但是quick sort希望尽可能的均分中间的数, 这样的话performance会好一些
{% endtab %}

{% tab title="Java" %}
```java
public class Solution {
    /**
     * @param nums: The integer array you should partition
     * @param k: An integer
     * @return: The index after partition
     */
    public int partitionArray(int[] nums, int k) {
        // write your code here
        if(nums == null || nums.length == 0){
          return 0;
        }
        
        int start = 0, end = nums.length - 1;
        int pivot = nums[start + (end - start) / 2];
        
        while(start <= end){
          while(start <= end && nums[start] < k){
            start++;
          }
          
          while(start <= end && nums[end] >= k){
            end--;
          }
          
          if(start <= end){
            int tmp = nums[start];
            nums[start] = nums[end];
            nums[end] = tmp;
            
            start++;
            end--;
          }
        }
        
        return start;
    }
}
```
{% endtab %}

{% tab title="Python" %}
```python
class Solution:
    """
    @param nums: The integer array you should partition
    @param k: An integer
    @return: The index after partition
    """
    def partitionArray(self, nums, k):
        # write your code here
        if nums == None or len(nums) == 0:
            return 0
            
        start = 0
        end = len(nums) - 1
        
        while start <= end:
            while start <= end and nums[start] < k:
                start += 1
            while start <= end and nums[end] >= k:
                end -= 1
            
            if(start <= end):
                tmp = nums[start]
                nums[start] = nums[end]
                nums[end] = tmp
              
                start += 1
                end -= 1
                
        return start
```
{% endtab %}
{% endtabs %}

