```JAVA
package easy_test;

/** 公众号:「一个不甘平凡的码农」
 * 1) 数组的插入、删除、按照下标随机访问操作；
 * 2）数组中的数据是int类型的；
 *
 * Author:小鹿
 */
/**
 * 测试数据注意事项：
 *
 * 插入数据：
 * 1、判断空数组插入数据。
 * 2、输入下标索引超出下标范围。
 * 3、将数据插入到尾部。
 * 
 * 查找数据：
 * 1、输入下标超出下标范围
 * 
 * 
 * 删除数据：
 * 1、索引超出下标范围。
 * 2、删除尾元素
 * 
 */


/**
 * 1) 数组的插入、删除、按照下标随机访问操作；
 * 2）数组中的数据是int类型的；
 *
 */

public class Array05 {
	
	  //声明变量
	  private int data[];
	  private int n;
	  private int count;
	  
	  public static void main(String[] args) {
		  Array05 array = new Array05(4);
		  //插入数据
		  array.insertHead(1);
		  System.out.println("插入数据:"+array.insert(1, 2));
		  array.insert(2, 3);
		  array.insert(3, 4);
		  //查找
		  System.out.println("查找数据:"+array.find(1));
		  //删除数据
		  System.out.println("删除数据:"+array.delete(4));
		  //打印所有数据
		  System.out.println("打印所有数据:");
		  array.printAll();
		  
	  }

	 /**
	  * @param capacity:用户传参，数组的大小
	  * 功能：构造函数（初始化数据）
	  */
	  public Array05(int capacity) {
		//定义一个大小为 capacity 的数组
	    data = new int[capacity];
	    n = capacity;
	    count = 0;
	  }
	  
	  /**
	   * 功能：插入头元素
	   * @param value 插入的元素值
	   * @return
	   */
	  public Boolean insertHead(int value) {
		  data[count] = value;
		  count++;
		  return true;
	  }
	  
	  /**
	   * 功能：数组插入元素
	   * @param index:数组下标索引
	   * @param value:要插入的元素值
	   * @return
	   */
	  public boolean insert(int index, int value) {
		//首先判断删除的索引值是否在数组索引范围内（边界问题）
	    if (index < 0 || index > count) return false;
	    //还要考虑到一种情况就是，如果你一直删除元素知道把元素全部删除完，数组长度为0，无法进行插入元素，对于这种情况就需要进行判断
	    if (count == n) {
	    	return false;
	    }
	    //数组中数据从最后一依次向后移动，直到将用户指定索引元素空出空间
	    for (int i = count - 1; i >= index; --i) {
	      data[i+1] = data[i];
	    }
	    //将元素插入到数组中
	    data[index] = value;
	    //数组长度+1
	    ++count;
	    return true;
	  }
	
	
	  /**
	   * 功能：下标随机访问
	   * @param index:用户传参下标
	   * @return
	   */
	  public int find(int index) {
		//索引判断，课程中所讲的边界问题（不在数组的范围内函数返回-1）
	    if (index < 0 || index > count ) return -1;
	    //否则返回该索引对应的数据
	    return data[index-1];
	  }
	  
	  /**
	   * 功能：根据用户输入索引删除数组中数据。
	   * @param index
	   * @return
	   */
	  public boolean delete(int index) {
		//首先判断删除的索引值是否在数组索引范围内（边界问题）
	    if (index < 0  || index > count) return false;
	    //将删除元素的后边元素都向前依次移动
	    for(int i = index; i < count; ++i) {
	      data[i-1] = data[i];
	    }
	    //删除一个元素后，数组长度 -1
	    --count;
	    return true;
	  }
	
	  /**
	   * 通过for循环输出数组所有元素
	   */
	  public void printAll() {
	    for (int i = 0; i < count; ++i) {
	      System.out.print(data[i] + " ");
	    }
	    System.out.println();
	  }
}


```

