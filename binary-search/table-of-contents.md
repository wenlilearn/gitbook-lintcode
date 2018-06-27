# Table of contents

在这个小节中, 我们主要学习Binary Search\(二分法\), 我使用的模板如下:

```java
public Solution {
  public int binarySearch(int nums, int target){
    if(nums == null || nums.length == 0){
      return -1;
    }

    int start = 0, end = nums.length - 1;

    // Find the first occurance of a target
    while(start + 1 < end){
      int mid = start + (end - start) / 2;

      if(nums[mid] >= target){
        end = mid;
      } else {
        start = mid;
      }
    }

    if(nums[start] == target){
      return start;
    } else if(nums[end] == target){
      return end;
    } else {
      return -1;
    }
  }
}
```

## 题目:

* [585. Maximum Number in Mountain Sequence](https://wenlilearn.gitbook.io/lintcode/~/edit/drafts/-LFzeUhbwYeS5ixZgD_q/binary-search/585.-maximum-number-in-mountain-sequence)
* [460. Find K Closest Elements](https://github.com/wenlilearn/gitbook-lintcode/tree/6f2c79f0ec15972131f3fb2d666beaa77bfb2284/binary_search/binary_search/460.-find-k-closest-elements.md)
* [447. Search in a Big Sorted Array](https://github.com/wenlilearn/gitbook-lintcode/tree/6f2c79f0ec15972131f3fb2d666beaa77bfb2284/binary_search/binary_search/447.-search-in-a-big-sorted-array.md)
* [428. Pow\(x, n\)](https://github.com/wenlilearn/gitbook-lintcode/tree/6f2c79f0ec15972131f3fb2d666beaa77bfb2284/binary_search/binary_search/428.-pow-x-n.md)

