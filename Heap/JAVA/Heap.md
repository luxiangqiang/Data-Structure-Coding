```java
package com.xiaolu.Heap;

/**
 * 公众号:「一个不甘平凡的码农」
 * 时间:2019/2/28
 * 功能:堆的插入与删除
 * @author 小鹿
 *
 */
public class Heap {
	//数组，从 1 开始存储
	private static int[] a;
	//记录堆可以存储的最大数据
	private int n;
	//记录已经存储的数据个数
	private int count;
	//初始化数据
	public Heap(int capacity) {
		a = new int[capacity + 1];
		n = capacity;
		count = 0;
	}
	
	public static void main(String[] args) {
		Heap heap = new Heap(5);
        //插入数据
		heap.insert(1);
		heap.insert(5);
		heap.insert(3);
		heap.insert(6);
		heap.print(a);
		//移除最大数据
		heap.removeMax();
		System.out.println("");
		heap.print(a);
		
	}
	
	
	/**
	 * 时间:2019/2/28
	 * 功能:插入数据
	 * 分析:
	 * 1)插入到数组尾部(堆最后的节点)
	 * 2)自下而上堆化(比较和交换)
	 * 边界条件:
	 * 1)判断是否已经堆满
	 * 2)
	 * @param data 插入的数据
	 */
	public void insert(int data) {
		//判断堆是否已满
		if(count >= n) return;
		//计数+1(下标 0 不存储数据)
		count++;
		//将数据插入最后节点
		a[count] = data;
		
		//自下往上堆化
		int i = count;
		//判断插入数据的根节点是否大于 0 且插入的数据是否大于根节点数据
		while(i/2 > 0 && a[i] > a[i/2]) {
			//交换下标为 i 和 i/2 的元素
			swap(a,i,i/2);
			//继续堆化比较交换
			i = i/2;
		}
	}
	
	/**
	 * 时间:2019/2/28
	 * 功能:删除堆顶数据
	 * 分析:
	 * 1)判断堆是否为空
	 * 2)数组长度 -1
	 * 3)从下标为 1 的数据从上到下进行堆化
	 * 4)在左右节点中选出最大元素进行交换
	 * 边界分析:
	 * 1)判断堆是否为空
	 * 2)堆中是否只有一个元素
	 * @param data 要删除的数据
	 */
	public void removeMax() {
		//如果堆中无数据,则返回
		if(count == 0) return;
		//删除堆顶的第一个元素,与最后一个元素进行交换
		a[1] = a[count];
		//数组长度-1
		count--;
		//从上到下进行堆化
		heapify(a,count,1);
	}
	/**
	 * 时间:2019/2/28
	 * 功能:从上自下堆化
	 * @param a 堆化的数组
	 * @param count 当前堆中的数据
	 * @param i 
	 */
	private void heapify(int[] a,int n,int i) {
		while(true) {
			int maxPos = i;
			//选择子节点中最大的数据作交换
			if(i*2 < n && a[i] < a[i*2]) maxPos = i*2;
			if(i*2+1 <= n && a[maxPos] < a[i*2+1]) maxPos = i*2+1;
			
			//如果堆顶只剩一个元素,break
			if(maxPos == i) break;
			
			//进行交换
			swap(a, i, maxPos);
			//继续往下堆化
			i = maxPos;
		}
	}

	/**
	 * 时间:2019/2/28
	 * 功能:遍历堆中的所有数据
	 * @param a 数组
	 */
	public void print(int[] a) {
		for (int i = 0; i < a.length; i++) {
			System.out.print(a[i]+ " ");
		}
	}

	/**
	 * 时间:2019/2/28
	 * 功能:进行数据交换
	 * @param a 数据 1
	 * @param b 数据 2 
	 */
	private void swap(int[] a, int x,int y) {
		int temp;
		temp = a[x];
		a[x] = a[y];
		a[y] = temp;
	}
}
```

