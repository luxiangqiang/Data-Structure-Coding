```java
package com.test.xiaolu;

/**
 * 二分查找
 * @author 小鹿
 *
 */
public class TwoFind {

	/**
	 * 思路：
	 * 1、在数组头、尾定义两个指针(low,height)
	 * 2、取中间数值mid
	 * 3、判断是否为查找值
	 * 4、如果不是，移动 mid 指针,变化low,height
	 * @param args
	 */
	public static void main(String[] args) {
		int[] a = {3,4,6,7,10};
		TwoFind tFind = new TwoFind();
		System.out.print("该数据的下标为:"+tFind.find4(a,5,5));
	}
	
	/**
	 * 功能:最简单的二分查找
	 * @param a 数组
	 * @param n 数组长度
	 * @param value 要查找的值
	 */
	public int simpleFind(int[] a,int n, int value) {
		int low = 0;
		int high = n - 1;
		
		// 当两个指针同时指向一个数据时，必须用 <=
		while(low <= high) {
			//注意:两者之和可能会溢出
			//改进: low + (high - low)/2 或 low + ((high - low)>>2)
			int mid = low + (high - low)/2;
			if(a[mid] == value) {
				return mid;
			}else if(a[mid] < value) {
				// 如果不 + 或 - 会发生死循环
				low = mid + 1;
			}else {
				high = mid - 1;
			}
		}
		return -1;
	}
	
	/**
	 * 功能:递归实现最简单的二分查找
	 * @param a 数据
	 * @param low 初始位置
	 * @param height 终止位置
	 * @param value 查找的值
	 * @return 
	 */
	public int recursionTwoFind(int[] a,int low,int high,int value) {
		//终止条件
		if(low > high) return -1;
		
		//计算中间结点
		int mid = low + (high-low)/2;
		
		//进行递归
		if(a[mid] == value) {
			return mid;
		}else if(a[mid] < value){
			return recursionTwoFind(a, mid + 1, high, value);
		}else {
			return recursionTwoFind(a, low, mid - 1, value);
		}
	}
	
	/**
	 * 变体一:查找第一个值等于给定值的元素
	 * @param a 数组
	 * @param n 数组的长度
	 * @param value 超找的值
	 * @return 该元素的数组下标
	 */
	public int find1(int[] a, int n, int value) {
		int low = 0;
		int high = n - 1;
		
		// 当两个指针同时指向一个数据时，必须用 <=
		while(low <= high) {
			//注意:两者之和可能会溢出
			//改进: low + (high - low)/2 或 low + ((high - low)>>2)
			int mid = low + (high - low)/2;
			if(a[mid] == value) {
				// 找出重复元素中第一个元素
				if(mid == 0 || a[mid - 1] != value) {
					return mid;
				}else {
					high = mid - 1;
				}
			}else if(a[mid] < value) {
				// 如果不 + 或 - 会发生死循环
				low = mid + 1;
			}else {
				high = mid - 1;
			}
		}
		return -1;
	}
	
	/**
	 * 变体一:查找最后一个值等于给定值的元素
	 * @param a 数组
	 * @param n 数组的长度
	 * @param value 超找的值
	 * @return 该元素的数组下标
	 */
	public int find2(int[] a, int n, int value) {
		int low = 0;
		int high = n - 1;
		
		// 当两个指针同时指向一个数据时，必须用 <=
		while(low <= high) {
			//注意:两者之和可能会溢出
			//改进: low + (high - low)/2 或 low + ((high - low)>>2)
			int mid = low + (high - low)/2;
			if(a[mid] == value) {
				// 找出重复元素中第一个元素
				if(mid == n - 1 || a[mid + 1] != value) {
					return mid;
				}else {
					low = mid + 1;
				}
			}else if(a[mid] < value) {
				// 如果不 + 或 - 会发生死循环
				low = mid + 1;
			}else {
				high = mid - 1;
			}
		}
		return -1;
	}
	
	/**
	 * 变体三:查找第一个大于等于给定值的元素
	 * @param a 数组
	 * @param n 数组的长度
	 * @param value 数组的值
	 * @return 
	 */
	public int find3(int[] a, int n, int value) {
		int low = 0;
		int high = n - 1;
		
		// 当两个指针同时指向一个数据时，必须用 <=
		while(low <= high) {
			// 注意:两者之和可能会溢出
			// 改进: low + (high - low)/2 或 low + ((high - low)>>2)
			int mid = low + (high - low)/2;
			if(a[mid] >= value) {
				if((mid == 0) || (a[mid - 1] < value )) {
					return mid;
				}else {
					high = mid - 1;
				}
			}else {
				low = mid + 1;
			}
		}
		return -1;
	}
	
	/**
	 * 变体四:查找第一个小于等于给定值的元素
	 * @param a 数组
	 * @param n 数组的长度
	 * @param value 数组的值
	 * @return 
	 */
	public int find4(int[] a, int n, int value) {
		int low = 0;
		int high = n - 1;
		
		// 当两个指针同时指向一个数据时，必须用 <=
		while(low <= high) {
			// 注意:两者之和可能会溢出
			// 改进: low + (high - low)/2 或 low + ((high - low)>>2)
			int mid = low + (high - low)/2;
			if(a[mid] <= value) {
				if((mid == n-1) || (a[mid + 1] > value )) {
					return mid;
				}else {
					low = mid + 1;
				}
			}else {
				high = mid - 1;
			}
		}
		return -1;
	}
}

```

