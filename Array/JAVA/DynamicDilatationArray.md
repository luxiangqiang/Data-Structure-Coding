```java
package com.test.xiaolu;
import javax.xml.crypto.Data;

/**
 * 功能：实现一个支持动态扩容的数组
 * 方法一:System.arraycopy()
 * 最好时间复杂度为O(1),最坏时间复杂度为 O(n),平均时间复杂度为 O(1).
 * 
 * 方法二:ArrayList 实现自动扩容
 * @author 小鹿
 *
 */


public class DynamicDilatationArray {
	private int count;
	private int[] array;
	private int num;
	private int n;
	
	//初始化
	public DynamicDilatationArray(int number) {
		count = 0;
		array = new int[number];
		num = number;
		n = 1;
	}
	
	
	public static void main(String[] args) {
		DynamicDilatationArray data = new DynamicDilatationArray(5);
		data.insert(1);
		data.insert(2);
		data.insert(3);
		data.insert(4);
		data.insert(5);
		data.insert(6);
		data.insert(7);
		data.insert(8);
		data.insert(9);
		data.insert(10);
		data.insert(11);
		data.insert(12);
		data.print();	
	}
	
	//插入数据
	public void insert(int value) {
		if(count>=num*n) {
			//动态扩容
			int[] newArray = new int[array.length*2];
			//数组数据搬移
			for(int j =0;j<array.length;j++) {
				newArray[j] = array[j];
			}
//			System.arraycopy(array, 0, newArray, 0, array.length);
			
			array = newArray;
			//然后再插入数组
			array[count] = value;
			//下标移动
			count++;
			//扩容计数
			n++;
		}else {
			//插入数据
			array[count] = value;
			//下标移动
			count++;
		}
	}
	
	//打印数组内容
	public void print() {
		for(int i=0;i<array.length;i++) {
			System.out.print(array[i]+" ");
		}
	}
}
```

