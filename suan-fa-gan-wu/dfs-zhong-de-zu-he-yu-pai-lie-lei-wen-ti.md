# DFS中的组合与排列类问题

### DFS中的组合类问题:

* 题目要求一般是从集合中选取某些元素, 使得这些元素满足一定的条件
* 一般需要记下index\(如果允许重复那么就是当前元素的index, 如果不允许重复就是后面元素的index\)
* 当index &gt; 数组长度的时候, 我们就可以退出了\(等于的情况也是合理的, 这个不要忘记了\)
* 去重是依靠i &gt; start && \[i\] == \[i - 1\]

### DFS中的排列类问题:

* 题目一般要求要求从某个集合中选出某些元素, 使得这些元素能排成一定的顺序
* 一般需要记下当前用了哪些元素
* 去重是通过i &gt; 0 && \[i\] == \[i - 1\]
* 让我们来看一种特殊的排列类问题, 求下一个排列. 算法如下:

  * 从后往前应该是一个递增序列, 如果我们碰到那个不是递增序列的那个数, 我们记下来它的index\(考虑如下情况: x, x, x, 7, 9, 6, 3, 我们知道9, 6, 3 这三个数无论怎么交换, 都没有办法使得组合变得更大, 所以我们需要找到前面的那个7, 如果把7交换过来的话, 那么7, 9, 6, 3就能变成9,3,6,7\)
  * 如果i &gt; 0, 那么从这个数开始, 找到后面比他大的第一个数\(从后往前找即可, 因为从数组结尾开始应该是一个递增序列, 这样交换了以后也可以保证是地增序列\)
  * 最后从交换的那个数后面开始到数组结尾进行一次reverse即可
  * 程序实现如下

  ```java
  public class Solution {
      /**
       * @param nums: An array of integers
       * @return: nothing
       */
      public void nextPermutation(int[] nums) {
          // write your code here
          if(nums == null || nums.length == 1){
            return;
          }
        
          int i = 0, j = 0;
        
          for(i = nums.length - 1; i > 0; i--){
            if(nums[i] > nums[i - 1]){
              break;
            }
          }
        
          if(i != 0){
            for(j = nums.length - 1; j > i; j--){
              if(nums[j] > nums[i - 1]){
                break;
              }
            }
          
            int tmp = nums[j];
            nums[j] = nums[i - 1];
            nums[i - 1] = tmp;
          }
        
          j = nums.length - 1;
        
          while(i <= j){
            int tmp = nums[j];
            nums[j] = nums[i];
            nums[i] = tmp;
            i++;
            j--;
          }
        
          return;
      }
  }
  ```

* 还有一类问题, 要求求排列的index, 即到当前位置的排列一共有几种?
  * 我们举个例子,  \[3,7,4,9,1\], 对于这个数字来说, 它之前的排列是:
    * \[3,7,4,1,?\]
    * \[3,7,1,?,?\]
    * \[3,1或者4,?,?,?\]
    * \[1,?,?,?,?\]
  * 那么对于每个数组中的数字来说, 我们可以这样找出它之前的排列:
    * 从i - 1开始, 找到从n到i - 1中比自己小的数字
    * 然后用这个数乘以后面数字的排列个数即可\(通常为\(n - i\)!\)
  * 程序实现如下:

    ```java
    public class Solution {
        /**
         * @param A: An array of integers
         * @return: A long integer
         */
        public long permutationIndex(int[] A) {
            // write your code here
            if(A == null){
              return 0;
            }
        
            if(A.length == 1){
              return 1;
            }
        
            long permutation = 1;
            long res = 0;
            int index = A.length - 2;
        
            while(index >= 0){
              int smaller_count = 0;
          
              for(int j = index; j < A.length; j++){
                if(A[j] < A[index]){
                  smaller_count++;
                }
              }
          
              res += smaller_count * permutation;
              permutation *= (A.length - index);
              index--;
            }
        
            return res + 1;
        }
    }
    ```

