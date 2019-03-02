```java
package com.test.xiaolu;

/**
 * 公众号:「一个不甘平凡的码农」
 * 时间:2019/3/2
 * 功能:循环队列
 * 1)入队
 * 2)出队
 * @author 小鹿
 *
 */
public class CircularQueue {
	//声明一个 int 队列
	private int[] items;
	private int n;
	
	//声明头、尾指针
	private int head = 0;
	private int tail = 0;
	
	//初始化变量
	public CircularQueue(int capacity) {
		items = new int[capacity];
		n = capacity;
	}
	
	public static void main(String[] args) {
		CircularQueue c = new CircularQueue(5);
		c.enqueue(1);
		c.enqueue(2);
		c.enqueue(3);
		c.enqueue(4);
		//循环队列有一个空闲空间,5不在队列中
		System.out.println(c.enqueue(5));
		c.dequeue();
		System.out.println(c.enqueue(5));
		c.print();
	}
	
	/**
	 * 时间:2019/3/2
	 * 功能:入队
	 * @param data 元素
	 */
	public Boolean enqueue(int data) {
		//队满
		if((tail+1)%n == head) return false;
		//入队
		items[tail] = data;
		//求下一空间
		tail = (tail+1) % n;
		return true;
	}
	
	/**
	 * 时间:2019/3/2
	 * 功能:出队
	 */
	public int dequeue() {
		//队空
		if(tail == head) return -1;
		//出队
		int temp = items[head];
		head = (head+1) % n;
		return temp;
	}
	
	/**
	 * 时间:2019/3/2
	 * 功能:打印队列
	 */
	public void print() {
		for (int i = 0; i < items.length; i++) {
			System.out.print(items[i]+" ");
		}
	}
}

```

