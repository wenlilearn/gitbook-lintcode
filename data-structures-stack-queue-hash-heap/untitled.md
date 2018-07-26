# 364. Trapping Rain Water II

{% tabs %}
{% tab title="Problem" %}
#### 364. Trapping Rain Water II

Given _n_ x _m_ non-negative integers representing an elevation map 2d where the area of each cell is _1_ x _1_, compute how much water it is able to trap after raining.

![](https://lintcode-media.s3.amazonaws.com/problem/trapping-rain-water-ii.jpg)

#### Example

Given `5*4` matrix

```text
[12,13,0,12]
[13,4,13,12]
[13,8,10,12]
[12,13,12,12]
[13,13,13,13]
```

return `14`.
{% endtab %}

{% tab title="Solution" %}
### Heap + BFS:

* 灌水类题目
* 这个题目的思路是这样的:
  * 把最外面一圈加入heap
  * 然后从heap中取高度最低的那个点
    * 看它上下左右四个点
      * 能灌水的高度等于当前点的高度减去碰到的点的高度\(要记住当前点组成的是围墙\)
        * 如果这个差是负的那么就计入0
      * 然后把后面的点放入heap中
  * 最后返回总共灌水的高度即可\(高度差之和\)
{% endtab %}

{% tab title="Java" %}
```java
class Point implements Comparable<Point> {
  int x, y, h;
  
  public Point(int x, int y, int h){
    this.x = x;
    this.y = y;
    this.h = h;
  }
  
  public int compareTo(Point p){
    return this.h - p.h;
  }
}

public class Solution {
    /**
     * @param heights: a matrix of integers
     * @return: an integer
     */
    public int trapRainWater(int[][] heights) {
        // write your code here
        if(heights == null || heights.length == 0 ||
        heights[0] == null || heights[0].length == 0){
          return 0;
        }
        
        int m = heights.length, n = heights[0].length;
        PriorityQueue<Point> heap = new PriorityQueue<>();
        boolean[][] visited = new boolean[m][n];
        
        for(int i = 0; i < m; i++){
          for(int j = 0; j < n ; j++){
            if(i == 0 || j == 0 || i == m - 1 || j == n - 1){
              heap.add(new Point(i, j, heights[i][j]));
              visited[i][j] = true;
            }
          }
        }
        
        int res = 0;
        int[] dx = {0, 0, -1, 1};
        int[] dy = {-1, 1, 0, 0};
        
        while(!heap.isEmpty()){
          Point cur = heap.remove();
          
          for(int i = 0; i < 4; i++){
            int nx = cur.x + dx[i];
            int ny = cur.y + dy[i];
            
            if(nx < 0 || nx >= m || ny < 0 || ny >= n ||
              visited[nx][ny]){
                continue;
              }
              
            visited[nx][ny] = true;
            res += Math.max(0, cur.h - heights[nx][ny]);
            //最后记住一定是cur和heights[nx][ny]之间最高的高度
            //这是因为heights[nx][ny]灌完了以后就相当于成为了墙
            heap.add(new Point(nx, ny, Math.max(cur.h, heights[nx][ny])));
          }
        }
        
        return res;
    }
}
```
{% endtab %}
{% endtabs %}

