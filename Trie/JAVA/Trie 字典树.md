```java
package com.xiaolu.Trie;

/**
 * 功能:字典树(Trie 树)
 * @author 小鹿
 *
 */
public class Trie {
	
	//Trie 树的结点
	 public class TrieNode {
		 
		//数据域: 存放的字符数据
	    public char data;
	    // 结点中存放的数组
	    public TrieNode[] children = new TrieNode[26];
	    //记录字符是否已经存放完毕
	    public boolean isEndingChar = false;
	    //构造函数(初始化)
	    public TrieNode(char data) {
	      this.data = data;
	    }
	  }
	  
	  // 存储无意义字符(根节点为'/')
	  private TrieNode root = new TrieNode('/'); 

	  /**
	   * 往 Trie 树中插入一个字符串
	   * @param text 要插入的字符串
	   */
	  public void insert(char[] text) {
		// p 结点存储为空
	    TrieNode p = root;
	    
	    //循环遍历字符串中的每个字符
	    for (int i = 0; i < text.length; ++i) {
	      //计算每个字符所在数组的下标
	      int index = text[i] - 'a';
	      //判断该下标的数据是否已存字符
	      if (p.children[index] == null) {
	    	//如果没有存放，我们就将该字符存入结点
	        TrieNode newNode = new TrieNode(text[i]);
	        //存放该结点
	        p.children[index] = newNode;
	      }
	      //将指针移动到该数组中的 TrieNode 结点
	      p = p.children[index];
	    }
	    //所有字符存放完毕之后，将值置为 true
	    p.isEndingChar = true;
	  }

	  /**
	   * 在 Trie 树中查找一个字符串
	   * @param pattern 要查找的字符串
	   * @return 
	   */
	  public boolean find(char[] pattern) {
		//定义根节点'/'
	    TrieNode p = root;
	    //遍历要查找的字符
	    for (int i = 0; i < pattern.length; ++i) {
	      //计算字符串中的第一个字符在数组中的下标
	      int index = pattern[i] - 'a';
	      //判断是否存在该字符
	      if (p.children[index] == null) {
	    	// 不存在 pattern
	        return false; 
	      }else {
	    	  //如果存在，将指针移动到该字符存储的数值中
	    	  p = p.children[index];
	      }
	    }
	    //判断匹配的该字符是否已经完全匹配
	    if (p.isEndingChar == false) {
	    	return false; // 不能完全匹配，只是前缀
	    } else {
	    	return true; // 找到 pattern
	    }
	  }
	}


```

