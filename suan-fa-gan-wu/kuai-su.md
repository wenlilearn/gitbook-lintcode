# 快速幂

{% tabs %}
{% tab title="Problem" %}
### 求x的n次方

* 给定一个x和一个n, 求x^n
{% endtab %}

{% tab title="Solution" %}
* 我们可以这么考虑, 如果我们想求x^n, 我们可以求x^\(n/2\)然后相乘即可
* 由此衍生出来了一种解法, 就是
  * 递归算出x^\(n/2\), 设为y
  * y \* y得出x^n
* 每次用O\(1\)的时间把问题分解成一半, 由此可以推导出解法的时间复杂度是O\(log\(n\)\)
{% endtab %}

{% tab title="Java - Recursive" %}
```java
int power(int x, int n){
    if(n == 0){
        return 1;
    }
    
    int local = power(x, n / 2);
    local = local * local;
    
    if(n % 2 == 1){
        local *= x;
    }
    
    return local;
}
```
{% endtab %}

{% tab title="Java - Iterative" %}
```java
int power(int x, int n){
    int ans = 1, base = x;
    
    while(n != 0){
        if(n % 2 == 1){
            ans *= base;
        }
        
        base *= base;
        n /= 2;
    }
    
    return ans;
}
```
{% endtab %}
{% endtabs %}

