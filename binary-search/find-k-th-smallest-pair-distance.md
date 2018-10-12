# Find K-th Smallest Pair Distance

{% tabs %}
{% tab title="Problem" %}
Given an integer array, return the k-th smallest **distance** among all the pairs. The distance of a pair \(A, B\) is defined as the absolute difference between A and B.

**Example 1:**  


```text
Input:
nums = [1,3,1]
k = 1
Output: 0 
Explanation:
Here are all the pairs:
(1,3) -> 2
(1,1) -> 0
(3,1) -> 2
Then the 1st smallest distance pair is (1,1), and its distance is 0.
```

**Note:**  


1. `2 <= len(nums) <= 10000`.
2. `0 <= nums[i] < 1000000`.
3. `1 <= k <= len(nums) * (len(nums) - 1) / 2`.
{% endtab %}

{% tab title="Solution" %}
### Binary Search:

* 最暴力的解法, 就是直接两个循环算出所有的distance, 排序, 然后选出第k个即可, 时间复杂度O\(n^2 + nlogn\)
* 聪明一点的办法, 既然我们想要知道这个distance, 我们完全可以通过二分答案来猜一个distance, 然后验证这个distance是不是满足要求即可, 伪代码如下:
  * 排序数组
  * 在0到最长distance之间进行二分, 选出一个distance
    * 算出这个小于等于这个distance的pair一共有多少
      * 如果小于k组, 那么我们就对右边进行二分
      * 如果大于k组, 那么我们就左边进行二分
  * 最后算出来一个distance, 使得小于等于它的pair个数是k个, 这个就是我们想要的
* 怎么算小于等于这个distance的pair个数?
  * 我们可以使用暴力的双循环, 只要见到两数之差小于distance的, 我们就可以把统计pair个数, 然后包括在最终的结果里面, 这样的话是O\(n^2 \* log\(n\)\)
  * 更聪明的办法, 是发现我们要找的, 是固定一边以后, 另一边的最小的index, 使得左边大于右边-猜的那个distance, 我们需要找到最小的这个左边的index, 然后用右边的index 减去左边这个index即可, 这样的话是O\(log\(n\) \* n\)
{% endtab %}

{% tab title="Java - Brute Force" %}
```java
class Solution {
    public int smallestDistancePair(int[] nums, int k) {
      if(nums == null || nums.length <= 1){
        return 0;
      }
      
      Arrays.sort(nums);
      
      int start = 0, end = nums[nums.length - 1] - nums[0];
      
      while(start < end){
        int mid = start + (end - start) / 2;
        int count = countDistancePairs(nums, mid);
        
        if(count < k){
          start = mid + 1;
        } else {
          end = mid;
        }
      }
      
      return end;
    }
  
  private int countDistancePairs(int[] nums, int mid){
    if(mid > nums[nums.length - 1] - nums[0]){
      return 0;
    }
    
    int res = 0;
    
    for(int i = 1; i < nums.length; i++){
      for(int j = 0; j < i; j++){
        if(nums[i] - nums[j] <= mid){
          res += i - j;
          break;
        }
      }
    }
    
    return res;
  }
}
```
{% endtab %}

{% tab title="Java - Binary Search" %}
```java
class Solution {
    public int smallestDistancePair(int[] nums, int k) {
      if(nums == null || nums.length <= 1){
        return 0;
      }
      
      Arrays.sort(nums);
      
      int start = 0, end = nums[nums.length - 1] - nums[0];
      
      while(start < end){
        int mid = start + (end - start) / 2;
        int count = countDistancePairs(nums, mid);
        
        if(count < k){
          start = mid + 1;
        } else {
          end = mid;
        }
      }
      
      return end;
    }
  
  private int countDistancePairs(int[] nums, int mid){
    if(mid > nums[nums.length - 1] - nums[0]){
      return 0;
    }
    
    int res = 0;
    
    for(int i = 1; i < nums.length; i++){
      res += i - lower(nums, i, nums[i] - mid);
    }
    
    return res;
  }
  
  private int lower(int[] nums, int right, int target){
    int start = 0, end = right - 1;
    
    while(start + 1 < end){
      int mid = start + (end - start) / 2;
      
      if(nums[mid] >= target){
        end = mid;
      } else {
        start = mid;
      }
    }
  
    if(nums[start] >= target){
      return start;
    } else if(nums[end] >= target){
      return end;
    } else {
      return right;
    }
  }
}
```
{% endtab %}
{% endtabs %}

