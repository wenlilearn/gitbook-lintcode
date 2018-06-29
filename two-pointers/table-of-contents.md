# Table of contents

在这一小节中, 我们会看到quick select以及quick sort的相关题目, 模板如下:
```Python
  # 我们select的是第k + 1小的数
  def quickSelect(numbers, start, end, k):
      # 结束条件是已经把范围缩小到最小了, 正是我们想要的数
      if start == end:
          return numbers[start]

      left = start
      right = end
      pivot = numbers[start + (end - start) / 2]

      while left <= right:
          #如果这里是单纯partition的话就是<=, 但是因为我们的模板是
          # quick sort/select, 所以这里写成了<
          while left <= right and numbers[left] < pivot:
              left += 1
          while left <= right and numbers[right] > pivot:
              right -= 1

          if left <= right:
              tmp = numbers[left]
              numbers[left] = numbers[right]
              numbers[right] = tmp
              left += 1
              right -= 1
    # 如果是quick sort, 那么这里的if就不需要了
      if k >= start and k <= right:
          return self.quickSelect(numbers, start, right, k)
      elif k >= left and k <= end:
          return self.quickSelect(numbers, left, end, k)
      else:
          return numbers[k]
```

* [228. Middle of Linked List](228.-middle-of-linked-list.md)
* [607. Two Sum III - Data structure design](607.-two-sum-iii-data-structure-design.md)
* [539. Move Zeroes](539.-move-zeroes.md)
* [521. Remove Duplicate Numbers in Array](521.-remove-duplicate-numbers-in-array.md)
* [464. Sort Integers II](464.-sort-integers-ii.md)
* [608. Two Sum II - Input array is sorted](608.-two-sum-ii-input-array-is-sorted.md)
* [143. Sort Colors II](143.-sort-colors-ii.md)
* [57. 3Sum](57.-3sum.md)
* [31. Partition Array](31.-partition-array.md)
* [5. Kth Largest Element](5.-kth-largest-element.md)
