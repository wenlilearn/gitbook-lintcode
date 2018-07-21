# Union Find\(并查集\)

### 并查集: 一种解决集合查询合并的数据结构

#### 原生操作:

* 判断两个元素在不在同一个集合中
* 合并两个集合

#### 派生操作:

* 查询某个元素所在集合元素个数\(这个需要单独的通过一个数组来记录\)
* 查询当前集合个数\(这个需要单独的一个变量来记录\)

#### 复杂度:

* 空间: O\(n\)
* Union\(\): O\(1\)
* find: O\(1\)

#### 代码模板:

* 数组版本

```java
class UnionFind {
    // father 数组用来存储集合间与元素间的关系
    // father里面实际上存的是这个集合的代表
    int father[];
    
    //初始话一个一共有n个元素的并查集
    public UnionFind(int n){
        father = new int[n];
        
        // 对于初始集合来说, 每个元素都在自己集合里
        for(int i = 0; i < n; i++){
            father[i] = i;
        }
    }
    
    //find操作找到这个元素所在的集合(包括路径压缩)
    public int find(int i){
        //如果这个元素所在的集合的代表就是自己, 直接返回自己即可
        if(father[i] == i){
            return i;
        }
        //如果这个元素所在的集合的代表不是自己, 那么就递归的寻找-
        //father数组对应的那个元素的所在的集合代表, 同时更新当前-
        //这个集合的代表
        father[i] = find(father[i]);
        
        return father[i];
    }
    
    //Union操作先看两个元素是不是在同一个集合中, 如果不在, 就把
    //他们放入一个集合中
    public void union(int a, int b){
        int father_a = find(a);
        int father_b = find(b);
        
        if(father_a != father_b){
            father[father_a] = father_b;
        }
    }
}


```

* 哈希表版本

```java
class UnionFind {
    // father 数组用来存储集合间与元素间的关系
    // father里面实际上存的是这个集合的代表
    Map<Integer, Integer> father;
    
    //初始话一个一共有n个元素的并查集
    public UnionFind(int n){
        father = new HashMap<Integer, Integer>();
        
        // 对于初始集合来说, 每个元素都在自己集合里
        for(int i = 0; i < n; i++){
            father.put(i, i);
        }
    }
    
    //find操作找到这个元素所在的集合(包括路径压缩)
    public int find(int i){
        //如果这个元素所在的集合的代表就是自己, 直接返回自己即可
        if(father.get(i) == i){
            return i;
        }
        //如果这个元素所在的集合的代表不是自己, 那么就递归的寻找-
        //father数组对应的那个元素的所在的集合代表, 同时更新当前-
        //这个集合的代表
        father.put(i, find(father.get(i)));
        
        return father.get(i);
    }
    
    //Union操作先看两个元素是不是在同一个集合中, 如果不在, 就把
    //他们放入一个集合中
    public void union(int a, int b){
        int father_a = find(a);
        int father_b = find(b);
        
        if(father_a != father_b){
            father.put(father_a, father_b);
        }
    }
}

```

* 哈希表版本可以更加灵活, 但是相对而言实际空间消耗可能更大

