```java
package easy_test;

/**
 * 功能:基本链表的链式栈，入栈、出栈、输出栈
 * @author : 小鹿
 *
 */
public class StackBasedLinkedList {
	//定义栈顶指针
	private Node top = null;
	
	//定义栈结点
	private static class Node {
		//栈结点数据域
	    private int data;
	    //栈结点指针域
	    private Node next;
	    //构造函数
	    public Node(int data, Node next) {
	      this.data = data;
	      this.next = next;
	    }
	    //get 获取数据域方法
	    public int getData() {
	      return data;
	    }
	}
	
	/**
	 * 功能:入栈
	 * @param value:要入栈的数据元素
	 */
	public void push(int value) {
		//创建一个栈结点 
	    Node newNode = new Node(value, null);
	    // 判断栈是否为空
	    if (top == null) {
	      //如果栈为空，就将入栈的值作为栈的第一个元素
	      top = newNode;
	    } else {
	      //否则插入到top栈结点前（所谓的就是单链表的头插法）
	      newNode.next = top;
	      top = newNode;
	    }
	}
	
	/**
	 * 功能 : 出栈
	 * @return: -1 为栈中没有数据
	 */
	public int pop() {
		// 如果栈的最顶层栈结点为null,栈为空
	    if (top == null) return -1;
	    
	    //否则执行出栈操作，现将栈顶结点的数据元素赋值给 Value
	    int value = top.data;
	    //将 top 指针向下移动
	    top = top.next;
	    //返回出栈的值
	    return value;
	}	
	
	/**
	 * 功能:输出栈中所有元素
	 */
	public void printAll() {
		//将栈顶指针赋值给p
	    Node p = top;
	    //循环遍历栈(遍历单链表)
	    while (p != null) {
	      System.out.print(p.data + " ");
	      //指向下一个结点
	      p = p.next;
	    }
	    System.out.println();
	}
}

```

