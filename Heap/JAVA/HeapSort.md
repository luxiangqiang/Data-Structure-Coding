```java
package com.xiaolu.Heap;

/**
 * 公众号：「一个不甘平凡的码农」
 * 时间:2019/2/28
 * 功能:堆排序
 * @author 小鹿
 *
 */
public class HeapSort {
	
	private static int[] a;
	private static int n;
	
	public HeapSort(int capitity) {
		a = new int[] {1,4,6,3,7,2};
		n = capitity;
	}
	
	public static void main(String[] args) {
		HeapSort heapSort = new HeapSort(6);
		heapSort.sort(a, n);
		heapSort.print();
	}
	
	/**
	 * 时间:2019/2/28
	 * 功能:建堆
	 * 1)取数组中间从后往前
	 * @param a 数组
	 * @param n 数组的大小
	 */
	public static void buildHeap(int[] a,int n) {
		for (int i = n/2; i >= 1; i--) {
			//倒数第二节点开始所有节点从上到下堆化
			heapify(a,n,i);
		}
	}
	/**
	 * 功能:从上自下堆化
	 * @param a 堆化的数组
	 * @param count 当前堆中的数据
	 * @param i 非叶子节点数据
	 */
	private static void heapify(int[] a,int n,int i) {
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
	 * 时间:2019/3/3
	 * 功能:堆排序
	 * 思路:大顶堆的堆顶数据最大，每次将堆顶的元素放到数据的尾部(也就是堆中删除数据的过程),先进行交换，然后进行从上到下堆化。
	 * 分析:
	 * 1)建堆(非叶子节点从上到下堆化)
	 * 2)排序(堆顶元素的删除)
	 * 边界条件:
	 * 1)堆内剩余数据是否大于1(交换)
	 * @param a 数组
	 * @param n 数据的个数
	 */
	public static void sort(int[] a, int n) {
	  //1、建堆
	  buildHeap(a, n);
	  
	  //2、排序
	  int k = n-1;
	  while (k > 1) {
	    //交换堆顶元素和最后一个元素
	    swap(a, 1, k);
	    //堆元素减一
	    --k;
	    //从上向下进行堆化
	    heapify(a, k, 1);
	  }
	}
	
	/**
	 * 功能:进行数据交换
	 * @param a 数据 1
	 * @param b 数据 2 
	 */
	private static void swap(int[] a, int x,int y) {
		int temp;
		temp = a[x];
		a[x] = a[y];
		a[y] = temp;
	}
	
	/**
	 * 时间:2019/3/3
	 * 功能:打印堆内数据
	 */
	public void print() {
		for (int i = 0; i < a.length; i++) {
			System.out.print(a[i]+" ");
		}
	}
}

```

