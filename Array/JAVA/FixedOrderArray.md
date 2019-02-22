```java
package com.test.xiaolu;
import java.util.concurrent.CountDownLatch;

/**
 * 实现一个大小固定的有序数组，支持动态增删改操作
 * @author 小鹿
 *
 */
public class FixedOrderArray {
	private int[] data;
	private int n;
	private int count;
	
	public FixedOrderArray(int n) {
		this.n = n;
		count = 0;
		data = new int[n];
	}
	
	public static void main(String[] args) {
		FixedOrderArray array02 = new FixedOrderArray(5);
		//插入
		array02.insert(1);//0
		array02.insert(3);//1
		array02.insert(2);//2
		array02.insert(1);//3
		array02.insert(0);//4
		//删除
		array02.delete(0);
		array02.print();
		//查找数据
		System.out.println();
		System.out.print("查找该数据的下标为:"+array02.find(2));
	}
	
	/**
	 * 功能：插入
	 * @param value 插入的元素
	 * @return 返回 Boolean 值
	 */
	public Boolean insert(int value) {
		//判断数组是否为空
		if(data == null && data.length==0) {
			return false;
		}else {
			//第一个数据直接插入数组
			if(count == 0) {
				data[count] = value;
				count++;
				return true;
			}
			//优化:先判断是否大于最后一个数据
			if(value>=data[count-1]) {
				data[count] = value;
				count++;
				return true;
			}
			//其他数据比较搬移
			for (int i = 0; i < data.length; i++) {
				if(value >= data[i]) {
					for (int j = count-1; j >= i+1; j--) {
						data[j+1] = data[j];
					}
					data[i+1] = value;
					count++;
					return true;
				}else {
					//插入数组第一个位置
					for (int j = count-1; j >=0; j--) {
						data[j+1] = data[j];
					}
					data[0] = value;
					count++;
					return true;
				}
			}
		}
		return false;
	}
	
	
	/**
	 * 功能:删除下标指定数据
	 * @param index 指定下标
	 * @return 返回删除的数据
	 */
	public int delete(int index) {
		//判断删除元素的下标是否合理
		if(index < 0 || index >= data.length) {
			return -1;
		}else {
			for (int i = index; i < count-1; i++) {
				data[i] = data[i+1];
			}
		}
		count--;
		return 0;
	}
	
	/**
	 * 功能: 查找 
	 * @param value 要查找的元素
	 * @return 返回该下标
	 */
	public int find(int value) {
		
		for (int i = 0; i <= count-1; i++) {
			if(data[i]==value) {
				return i;
			}
		}
		return -1;
	}
	
	//打印数组内容
	public void print() {
		for(int i=0;i<count;i++) {
			System.out.print(data[i]+" ");
		}
	}
}
```

