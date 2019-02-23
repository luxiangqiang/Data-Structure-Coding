```java
package com.test.xiaolu;


/**
 * 公众号:「一个不甘平凡的码农」
 * @author 小鹿
 * 功能:
 * [插入]
 * 1) 向单链表尾部添加数据
 * 2) 头插法
 * 3) 插入到指定结点的后边
 * 4) 插入到指定结点的前边
 * [删除]
 * 1) 删除尾部数据
 * 2) 删除指定结点
 * 3) 删除指定值结点
 * [查找]
 * 1) 单链表按值查找
 * 2) 按照索引查找 
 * 3) 遍历所有数据
 */
public class SinglyLinkedList {
	
	public static void main(String[] args) {
		SinglyLinkedList s = new SinglyLinkedList();
		s.inserValue(1);
		s.inserValue(2);
		s.inserValue(3);
		System.out.println("按值查找:"+s.findByValue(3));
		System.out.println("按索引查找:"+s.findByIndex(2));
//		s.deleteToTail();
		s.print();
	}
	
	//定义链表结点
	public class Node {
		//数据域
		int data;
		//指针域
		Node next;
		//初始化
		public Node(int data,Node next) {
			this.data = data;
			this.next = next;
		}
	}
	
	//设置头结点为空
	private Node head = null;
	
	/**
	 * 功能:构建新结点
	 * @param value
	 */
	public void inserValue(int value) {
		Node newNode = new Node(value, null);
		inserToTail(newNode);
	}
	
	/**
	 * 功能:向单链表尾部添加数据
	 * 边界条件:
	 * 1、判断是否是空链表(如果是，则将新结点赋值给 head)
	 * 
	 * @param value 数据元素
	 */
	public void inserToTail(Node newNode) {
		//判断是否为空链表
		if(head == null){
		   //将新结点直接赋给 head
           head = newNode;
           return;
        }
		Node p = head;
		while(p.next != null) {
			p = p.next;
		}
		
		p.next = newNode;
	}
	
	
	/**
	 * 时间:2019/2/22
	 * 功能:头插法
	 * 边界条件:
	 * 1、判断链表是否为空链表
	 * @param newNode 插入的结点
	 */
	public void createNewNode(int value) {
		Node newNode = new Node(value, null);
		inserToHead(newNode);
	}
	public void inserToHead(Node newNode) {
		//如果链表是空链表
		if(head == null) {
			//将新结点作为头部
			head = newNode;
		}else {
			//现将新节点的next指向头结点地址
			newNode.next = head;
			//将新结点替换成头部
			head = newNode;
		}
	}
	
	/**
	 * 时间:2019/2/22
	 * 功能:将元素插入到指定结点后边
	 * 边界条件:
	 * 1、判断指定结点是否为 null
	 * 
	 * @param p 指定的结点
	 * @param newNode 插入的结点
	 */
	public void inserAfter(Node p,int value) {
		Node newNode = new Node(value, null);
		insertAfter(p,newNode);
	}
	public void insertAfter(Node p,Node newNode) {
		//如果指定的结点为空(如果是空链表,头结点也等于 null),则返回
		if(p == null) return;
		//将原本 p 结点存储下一结点的地址赋值给新结点的地址域
		newNode.next = p.next;
		//然后p结点的地址域指向新结点
		p.next = newNode;
	} 
	
	 /**
	   * 时间:2019/2/22
	   * 功能:插入结点到指定结点前
	   * 边界条件:
	   * 1、判断指定结点 p 是否为 null
	   * 2、判断指定结点是否为头结点(头插法)
	   * 3、循环遍历找到指定结点的前一结点信息
	   * @param p 指定结点
	   * @param newNode 插入的结点
	   */
	  public void insertBefore(Node p, int value) {
		//生成新结点
	    Node newNode = new Node(value, null);
	    //插入到指定结点前边
	    insertBefore(p, newNode);
	  }
	  public void insertBefore(Node p,Node newNode) {
		  //如果指定的结点为空,则返回
		  if(p == null) return;
		  //判断是否为头结点 
		  if(head == p) {
			  inserToHead(newNode);
			  return;
		  }
		  
		  Node q = head;
		  //如果 head 为空链表。返回null
		  if(q == null) return; 
		  //循环遍历找到指向 p 结点的前一个结点
		  while(q != null && q.next != p) {
			  q = q.next;
		  }
		  //添加结点
		  newNode.next = q.next;
		  q.next = newNode;
	  }
	
	/**
	 * 功能:删除尾部数据
	 * 分析:
	 * 1、判断是否为空链表
	 * 2、循环遍历找到最后结点
	 */
	public void deleteToTail() {
		//如果链表为空链表,返回return
		if(head == null) return;
		Node p = head;
		Node q = null;
		//循环遍历找到最后结点
		while(p.next != null) {
			q = p;
			p = p.next;
		}
		//将最后结点的前一结点设置为空
		q.next = null;
	}
	
	/**
	 * 时间:2019/2/23
	 * 功能:删除指定结点
	 * 边界条件:
	 * 1、判断删除结点 p 是否为 null
	 * 2、判断链表是否为空
	 * 3、判断删除的结点是否为头结点(重新指定头结点)
	 * 4、判断是否循环到链尾,是否找到 p 结点
	 * @param p 指定结点
	 */
	public void deleteByNode(Node p) {
		//如果该结点为空,直接返回
		if(p == null) return;
		
		//如果链表为空,返回
		if(head == null) return;
		
		//如果删除的结点为头结点
		if(p == head) {
			//设置下一结点为头结点
			head = head.next;
		}

		//循环遍历找到 p 的前一结点
		Node q = head;
		//注意:这里是两种终止条件,1、没有找到该结点(q==null) 2、找到了该结点
		while(q != null && q.next != p) {
			q = q.next;
		}
		
		//如果到链表尾部没有找到 p 结点
		if(q == null) {
			return;
		}
		//删除 p 结点
		q.next = p.next;
	}
	
	/**
	 * 时间:2019/2/23
	 * 功能:删除指定值的结点
	 * 边界条件:
	 * 1、判断是否为空链表
	 * 2、遍历找到该值同时记录该结点的前一个节点
	 * @param value 删除的值
	 */
	public void deleteByValue(int value) {
		//如果链表为空,则返回
		if(head == null)  return;
		
		//循环遍历找到该值
		Node p = head;
		Node q = null;//用来记录该值结点的前一个节点
		while(p != null && p.data != value) {
			q = p;
			p = p.next;
		}
		//删除结点
		q.next = p.next;
	}
	
	/**
	 * 时间:2019/2/22
	 * 功能:单链表按值查找
	 * @param value 查找的值
	 * @return 返回该结点
	 */
	public Node findByValue(int value) {
		//将链表头部赋值给 p
		Node p = head;
		
		//循环遍历链表查找该值
		while(p != null && p.data != value) {
			p = p.next;
		}
		//判断 p 是否为 null,然后判断 p.data 的值为多少
		return p;
	}
	
	/**
	 * 时间:2019/2/22
	 * 功能:按照索引查找
	 * @param index 索引(1 开始)
	 * @return 返回该结点
	 */
	public Node findByIndex(int index) {
		Node p = head;
		//用来记录索引值
		int pos = 1;
		//循环遍历
		while(p != null && pos != index) {
			p = p.next;
			pos++;
		}
		//返回 p 结点
		return p;
	}
	
	/**
	 * 功能:打印所有链表结点
	 */
	public void print() {
		Node p = head;
		
		while(p != null) {
			System.out.print(p.data+" ");
			p = p.next;
		}
	}
}
```

