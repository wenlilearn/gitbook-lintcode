# Guaranteed Binary Search

{% tabs %}
{% tab title="Problem" %}
### Guaranteed Binary Search

We are given an unsorted array of n distinct elements. Use binary search to find a specific number. Which numbers are guaranteed to be able to be found using binary search in the array?

For example: Given \[2,1,3,4,6,5\] target = 5, we cannot find 5. Because when the random index is 5, we get element 6, then right pointer will move left, so we'll lose the opportunity to find target 5.

Given \[2,1,3,4,5,6\] target = 5, we can find 5. Because wherever the random index picks, we'll find target at last.

In \[2,1,3,5,4,6\], 3 and 6 are the numbers guaranteed to be found. In \[1,2,3\], all the numbers guaranteed to be found. In \[3,2,1\], no numbers guaranteed to be found.
{% endtab %}

{% tab title="Solution" %}
让我们观察一下这样的数字有什么特点, 举个很简单的例子:

\[1,2,3\]

2比1大, 2比3小, 所以2可以

再比如:

\[1,2,3,4,5\]

3比左边最大的数2大, 3又比右边最小的数4小, 所以可以

再比如:

\[5,4,3,2,1\]

3比左边最大的数小, 3比右边最大的数大, 这个就不行了

由此我们可以得出结论, 只要一个数比左边的最大值大, 而且比右边的最大值小, 那么我们就可以对这个数字进行二分查找
{% endtab %}

{% tab title="Java" %}
```java
/**
 * We are given an unsorted array of n distinct elements. Use binary search to find a specific number.
 * Which numbers are guaranteed to be able to be found using binary search in the array?
 * 
 * For example: Given [2,1,3,4,6,5] target = 5, we cannot find 5. Because when
 * the random index is 5, we get element 6, then right pointer will move left,
 * so we'll lose the opportunity to find target 5.
 * 
 * Given [2,1,3,4,5,6] target = 5, we can find 5. Because wherever the random
 * index picks, we'll find target at last.
 * 
 * In [2,1,3,5,4,6], 3 and 6 are the numbers guaranteed to be found.
 * In [1,2,3], all the numbers guaranteed to be found.
 * In [3,2,1], no numbers guaranteed to be found.
 */
class Solution {
  // Given a series of numbers, return the number of elements that can be binary searched
  public static int guaranteedBinarySearch(int[] nums) {
    if(nums == null){
      return 0;
    } 

    int n = nums.length;

    int left = 0;
    int[] left_max = new int[n];
    for(int i = 0; i < n; i++){
      left = Math.max(left, nums[i]);
      left_max[i] = left;
    }

    int right = nums[n - 1];
    int[] right_min = new int[n];
    for(int i = n - 1; i >= 0; i--){
      right = Math.min(right, nums[i]);  
      right_min[i] = right;
    }

    int ans = 0;
    for(int i = 0; i < n; i++){
      if(i == 0){
        if(nums[i] <= right_min[i]){
          ans++;  
        }
        continue;
      } 

      if(i == n - 1){
        if(nums[i] >= left_max[i]){
          ans++;  
        }  

        continue;
      }

      if(nums[i] >= left_max[i] && nums[i] <= right_min[i]){
        ans++;  
      }
    }

    return ans;
  }

  public static void main(String[] args) {
    int[][] cases = {
      {1,2,3}, //3
      {3,2,1}, //0
      {2,1,3,4,5,6}, //4
      {2,1,3,5,4,6}  //2
    };

    for(int[] c : cases){
      System.out.println(guaranteedBinarySearch(c));  
    }
  }
}

```
{% endtab %}
{% endtabs %}

