```java
package com.test.xiaolu;

import java.util.concurrent.ForkJoinPool.ManagedBlocker;

/**
 * 公众号:「一个不甘平凡的码农」
 * 时间:2019/3/2
 * 功能:队列
 * 1)入队
 * 2)出队
 * @author 小鹿
 *
 */

public class Queue {
	
	//声明一个 int 队列
	private int[] items;
	private int n;
	
	//声明头、尾指针
	private int head = 0;
	private int tail = 0;
	
	//初始化变量
	public Queue(int capacity) {
		items = new int[capacity];
		n = capacity;
	}
	
	public static void main(String[] args) {
		Queue queue = new Queue(5);
		//入队
		queue.enqueue2(1);
		queue.enqueue2(2);
		queue.enqueue2(3);
		queue.enqueue2(4);
		queue.enqueue2(5);
		//出队
		queue.dequeue();
		queue.dequeue();
		//搬移数据入队
		queue.enqueue2(6);
		queue.enqueue2(7);
		queue.print();
	}
	
	/**
	 * 时间:2019/3/2
	 * 功能:入队
	 * 存在的不足:浪费内存空间
	 * @param data 元素
	 */
	public Boolean enqueue(int data) {
		//队满
		if(tail == n) return false;
		//入队
		items[tail] = data;
		//指针向后移动
		tail++;
		return true;
	}
	
	/**
	 * 功能:优化后入队
	 * 边界分析:
	 * 1)判断队满
	 * 2)判断数据是否可向前移动
	 * @param data 元素
	 */
	public Boolean enqueue2(int data) {
		//队满
		if(tail == n) {
			if(head == 0) {
				return false;
			}else {
				//数据搬移(技巧)
				for (int i = head; i < tail; i++) {
					items[i - head] = items[i];
				}
				tail = tail - head;
				head = 0;
			}
		}
		//插入数据
		items[tail] = data;
		tail++;
		return true;
	}
	
	/**
	 * 时间:2019/3/2
	 * 功能:出队
	 * 存在的不足:浪费内存空间
	 */
	public int dequeue() {
		//队空
		if(head == tail) return -1;
		//出队
		int temp = items[head];
		head++;
		return temp;
	}
	
	/**
	 * 功能:打印队列
	 */
	public void print() {
		for (int i = head; i < tail; i++) {
			System.out.print(items[i]+" ");
		}
	}
}
```

