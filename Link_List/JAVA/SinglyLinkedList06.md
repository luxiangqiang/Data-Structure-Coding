```java
package easy_test;

/**
 * 1）单链表的插入、删除、查找操作；
 * 2）链表中存储的是int类型的数据；
 *
 * Author：小鹿
 */
 
public class SinglyLinkedList {
	
	/**
	 * 功能：定义 Node 结点，Node 包含数据域和引用（作用：存储所指向对象的内存地址）
	 * @author Boy Baby
	 *
	 */
	 public static class Node {
		//数据域
	    private int data;
	    //引用（存储所指向对象的内存地址）
	    private Node next;
	    //构造函数（初始化数据）
	    public Node(int data, Node next) {
	      this.data = data;
	      this.next = next;
	    }
	    //获取结点数据元素
	    public int getData() {
	      return data;
	    }
	  }
	 

	  private Node head = null;      
	  
	  /**
	   * 功能：单链表按值查找
	   * @param value
	   * @return
	   */
	  public Node findByValue(int value) {
		//将链表的头部复制给结点 p（？）
	    Node p = head;
	    //判断结点 p 是否为空相当于判断链表是否为空链表且结点中的值是否和要查找的值是否相同
	    while (p != null && p.data != value) {
	      //如果不相同，则将下一结点的地址赋值给 p
	      p = p.next;
	    }
	    //返回结点 p
	    //思考：如果单链表中没有要查找的数据怎么办？这个函数还合适吗？
	    return p;
	  }

	  /**
	   * 功能:单链表按照索引查找
	   * @param index:索引 0 是第一个元素
	   * @return
	   */
	  public Node findByIndex(int index) {
		//将链表的头部复制给结点 p（？）
	    Node p = head;
	    //定义计数变量 pos
	    int pos = 0;
	    //如果单链表不是空链表且索引不为用户指定索引
	    while (p != null && pos != index) {
	      //则将下一结点的地址赋值给 p
	      p = p.next;
	      //计数索引+1
	      ++pos;
	    }
	    //返回结点 p
	    //思考：如果单链表中没有要查找的数据怎么办？这个函数还合适吗？
	    return p;
	  }

	  /**
	   * 功能:将元素插入结点并且利用「头插法」插入链表
	   * @param value:结点插入元素值
	   */
	  public void insertToHead(int value) {
		//生成新结点
	    Node newNode = new Node(value, null);
	    //调用头插法函数
	    insertToHead(newNode);
	  }

	  /**
	   * 功能：头插法
	   * 	  ① 如果链表是空链表（head == null）,需要将新结点作为头部
	   *      ② 如果链表不是空链表,现将新节点的next指向头结点地址，然后将新结点替换成头部
	   * @param newNode:要插入的新节点
	   */
	  public void insertToHead(Node newNode) {
	  //如果链表是空链表
	  if (head == null) {
		 //将新结点作为头部
	     head = newNode;
	    } else {
	      //现将新节点的next指向头结点地址
	      newNode.next = head;
	      //将新结点替换成头部
	      head = newNode;
	    }
	  }
	  
	  /**
	   * 功能:将元素插入结点并且插入到指定结点的后面
	   * @param p:指定结点
	   * @param value:被插入结点的值域中的元素
	   */
	  public void insertAfter(Node p, int value) {
		//生成新结点
	    Node newNode = new Node(value, null);
	    //插入到指定结点后边
	    insertAfter(p, newNode);
	  }

	  /**
	   * 功能:插入到指定结点的后面
	   * 思考:如果该指定结点是最后一个结点，该方法是否适用？答:可行
	   * @param p:指定结点
	   * @param newNode:被插入的新结点
	   */
	  public void insertAfter(Node p, Node newNode) {
		//判断要插入的链表是否是一个空链表
	    if (p == null) return;
	    //将原本 p 结点存储下一结点的地址赋值给新结点的地址域
	    newNode.next = p.next;
	    //然后p结点的地址域指向新结点
	    p.next = newNode;
	  }

	  /**
	   * 功能:将元素插入结点并且插入到指定结点的前边
	   * @param p:指定结点
	   * @param value:被插入结点的值域中的元素
	   */
	  public void insertBefore(Node p, int value) {
		//生成新结点
	    Node newNode = new Node(value, null);
	    //插入到指定结点前边
	    insertBefore(p, newNode);
	  }

	  /**
	   * 功能:插入到指定结点的前边
	   * @param p:指定结点
	   * @param newNode:被插入结点的值域中的元素
	   */
	  public void insertBefore(Node p, Node newNode) {
		//判断要插入的链表是否是一个空链表  
	    if (p == null) return;
	    //判断指定的结点是否为头结点
	    if (head == p) {
    	  //头插法
	      insertToHead(newNode);
	      return;
	    }
	    
	    // 将单链表表头赋值给结点 q
	    Node q = head;
	    
	    //如果此单链表为空链表，停止操作
	    if (q == null) {
		      return;
		}
	    
	    // 通过结点 q 进行遍历查找到 p 结点
	    while (q != null && q.next != p) {
	      q = q.next;
	    }

	    //将p结点的地址存进新结点的地址域
	    newNode.next = p;
	    //将新结点的地址存进q结点的地址域
	    q.next = newNode;
	  }

	  /**
	   * 功能：指点结点删除
	   * @param p:指定的结点
	   */
	  public void deleteByNode(Node p) {
		//如果是空链表，直接return
	    if (p == null || head == null) return;

	    //如果指定的结点为头结点
	    if (p == head) {
	      //设置下一节点为头结点(所说的头结点为第二段)
	      head = head.next;
	      //问题:是否可以return？（可以return）
	      return;
	    }

	    //将存储头结点的地址赋值 q
	    Node q = head;
	    //如果链表不为空链表且地址域存储的值不为指定删除结点的地址就继续执行 while 循环
	    while (q != null && q.next != p) {
	      //下一个结点赋值给  q 结点
	      q = q.next;
	    }

	    //如果遍历到链表尾部还没有找到指定删除的结点，就 return。
	    if (q == null) {
	      return;
	    }
	    
	    //如果找到了，就删除p结点，也就是将该删除的结点下一结点的地址赋值给删除结点前的地址域存储
	    //q.next = p.next 与下边等式等价
	    q.next = q.next.next;
	  }

	  /**
	   * 功能:指定元素值删除链表结点
	   * @param value:指定的元素值
	   */
	  public void deleteByValue(int value) {
		//如果链表为空链表，则就return
	    if (head == null) return;
	    
	    //将存储头结点的地址赋值 q
	    Node p = head;
	    
	    Node q = null;
	    
	    //如果不是空链表且当前结点的元素值不等于指定元素的值，继续执行while循环
	    while (p != null && p.data != value) {
	      //将 p 结点赋值给 q 结点
	      q = p;
	      //然后将下一个结点赋值给 p 结点 
	      p = p.next;
	    }
	    
	    //如果遍历完单链表没有找到存储该元素的结点，就return。
	    if (p == null) return;

	    //如果单链表为空链表（？）
	    if (q == null) {
	      head = head.next;
	    } else {
	      //如果找到了，就删除p结点，也就是将该删除的结点下一结点的地址赋值给删除结点前的地址域存储
		  //q.next = p.next 与下边等式等价
	      q.next = q.next.next;
	    }
	  }
	  
	  //打印链表结点中所有数据结点
	  public void printAll() {
	    Node p = head;
	    
	    //由于链表最后一个存储的结点为null,所以不到
	    while (p != null) {
	      System.out.print(p.data + " ");
	      p = p.next;
	    }
	    System.out.println();
	  }
}



```

