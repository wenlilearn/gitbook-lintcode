# Trie\(字典树\)

作为一种常见的数据结构, 主要支持的操作是:

1. 在树中添加一个单词
2. 查找一个前缀在不在树中
3. 查找一个单词在不在树中

```java
class TrieNode {
    Map<Character, TrieNode> children;
    char c;
    boolean is_word;
    
    public TrieNode(char c){
        this.children = new HashMap<Character, TrieNode>();
        this.is_word = false;
        this.c = c;
    }
}

class Trie {
    TrieNode root;
    
    public Trie(){
        this.root = new TrieNode('\0');
    }
    
    public void add_word(String word){
        if(word == null){
            return;
        }
        
        TrieNode cur = root;
        char[] chars = word.toCharArray();
        
        for(char c : chars){
            if(cur.children.containsKey(c)){
                cur = cur.children.get(c);
            } else {
                TrieNode new_node = new TrieNode(c);
                cur.children.put(c, new_node);
                cur = new_node;
            }
        }
        
        cur.is_word = true;
        return;
    }
    
    public boolean has_prefix(String prefix){
        if(prefix == null){
            return false;
        }
        
        TrieNode cur = this.root;
        char[] chars = prefix.toCharArray();
        
        for(char c : chars){
            if(cur.children.containsKey(c)){
                cur = cur.children.get(c);
            } else {
                return false;
            }
        }
        
        return true;
    }
    
    public boolean has_word(String word){
        if(word == null){
            return false;
        }
        
        TrieNode cur = this.root;
        char[] chars = word.toCharArray();
        
        for(char c : chars){
            if(cur.children.containsKey(c)){
                cur = cur.children.get(c);
            } else {
                return false;
            }
        }
        
        return cur.is_word;
    }
}
```

