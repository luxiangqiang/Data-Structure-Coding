```JAVA
package easy_test;

/**
 * 1) 数组的插入、删除、按照下标随机访问操作；
 * 2）数组中的数据是int类型的；
 *
 * Author:小鹿
 */

public class Array05 {
	
	//声明变量
	  private int data[];
	  private int n;
	  private int count;

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
	   * 功能：下标随机访问
	   * @param index:用户传参下标
	   * @return
	   */
	  public int find(int index) {
		//索引判断，课程中所讲的边界问题（不在数组的范围内函数返回-1）
	    if (index < 0 || index >= count ) return -1;
	    //否则返回该索引对应的数据
	    return data[index];
	  }
	  
	  /**
	   * 功能:小鹿改进数组下标随机访问
	   * 改进内容:index 与上述函数不同，该  index 一般表示用户访问的位于数组的第几个元素
	   * 		对应的索引数据下标应该 -1 ，比如，访问第1个元素，在数组中对应的数据下标就是
	   * 		data[0],1 就是相当于用户输入的index。上述用户输入访问第一个元素直接输入0，
	   * 		index就是0，个人认为改进的更为符合实际操作罢了，原理还是一样的，改进如下代码。
	   * @param index
	   * @return
	   */
	  public int improvmentFind(int index) {
		   //索引判断，课程中所讲的边界问题（不在数组的范围内函数返回-1）
	       if (index-1 < 0 || index-1 >= count ) return -1;
	       //否则返回该索引对应的数据
	       return data[index-1];
	  }
	  
	  /**
	   * 功能：根据用户输入索引删除数组中数据。
	   * 补充：这个索引也是可以改进的，自己可以仿照上边改进一下
	   * @param index
	   * @return
	   */
	  public boolean delete(int index) {
		//首先判断删除的索引值是否在数组索引范围内（边界问题）
	    if (index < 0  || index >= count) return false;
	    //将删除元素的后边元素都向前依次移动
	    for(int i = index + 1; i < count; ++i) {
	      data[i-1] = data[i];
	    }
	    //删除一个元素后，数组长度 -1
	    --count;
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
	    if (index < 0 || index >= count) return false;
	    //还要考虑到一种情况就是，如果你一直删除元素知道把元素全部删除完，数组长度为0，无法进行插入元素，对于这种情况就需要进行判断
	    if (count == n) return false;
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
	   * 功能：插入的另一种情况，当我们向一个数组的尾部插入元素时，上述的插入方法就不适合了，所以我们单独写一个将元素插入到数组尾部的方法。
	   * @param value:要插入的元素值
	   * @return
	   */
	  public boolean insertToTail(int value) {
	    if (count == n) return false;
	    //在数组尾部追加空间，将新元素插入到数组尾部
	    data[count++] = value;
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

