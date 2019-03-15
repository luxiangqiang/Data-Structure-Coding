```java
package com.test.xiaolu;


/**
 * 2019/3/15
 * 公众号: 「一个不甘平凡的码农」
 * 归并排序
 * @author 小鹿
 *
 */
public class MergeSort {
	public static void main(String[] args) {
		MergeSort mSort = new MergeSort();
		int[] a = new int[] {4,3,7,2,9,1};
		mSort.mergeSort(a,0,a.length-1);
		for (int i = 0; i < a.length; i++) {
			System.out.print(a[i]);
		}
	}
	
	/**
	 * 时间：2019/3/15
	 * 功能:递归分治数据
	 * @param a 要分治的数组
	 * @param p	数组起始位置
	 * @param r 数组终止位置
	 */
	public void mergeSort(int[] a,int p,int r) {
		//终止条件
		if(p >= r) return;
		
		//取p到r之间的中间位置q,防止（p+r）的和超过int类型最大值
		int q = p + (r - p)/2;
		
		//递归分治
		mergeSort(a,p,q);
		mergeSort(a,q+1,r);
		
		//两个有序数组的合并
		merge(a, p, q, r);
		
	}
	
	/**
	 * 时间：2019/3/15 
	 * 功能: 合并 mergr
	 * @param a 要合并的数组
	 * @param p 数组起始的下标
	 * @param q	第二个数组起始的下标
	 * @param r 数组结束的下标
	 */
	public void merge(int[] a,int p,int q,int r) {
		int i = p,j = q+1,k = 0;
		int[] temp = new int[r-p+1];
		
		//两个有序数组合并
		while(i <= q && j <= r) {
			if(a[i] <= a[j]) {
				temp[k++] = a[i++];
			}else {
				temp[k++] = a[j++];
			}
		}
		
		int s = i;
		int e = q;
		if(j <= r) {
			s = j;
			e = r;
		}
		
		//剩余的数据添加到尾部
		while(s <= e) {
			temp[k++] = a[s++];
		}
		
		//将 temp 数据搬移到原数组
		for (int l = 0; l <= r-p; l++) {
			a[p+l] = temp[l];
		}
	}
}
```

