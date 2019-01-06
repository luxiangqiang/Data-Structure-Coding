```java
package easy_test;

/**
 * 公众号:「一个不甘平凡的码农」
 * 功能:用数组实现的队列
 * @author 小鹿
 *
 */
public class ArrayQueue {
	  //数组：items，数组大小：n
	  private String[] items;
	  private int n = 0;
	  
	  //head 表示队头下标，tail 表示队尾下标
	  private int head = 0;
	  private int tail = 0;

	  //初始化:申请一个大小为capacity的数组
	  public ArrayQueue(int capacity) {
	    items = new String[capacity];
	    n = capacity;
	  }

	  /**
	   * 功能:入队
	   * @param item 数组
	   * @return 是否插入成功
	   */
	  public boolean enqueue(String item) {
	    // 如果tail == n 表示队列已经满了
	    if (tail == n) return false;
	    //向数组中插入该元素
	    items[tail] = item;
	    //尾指针向后移动
	    ++tail;
	    //返回ture
	    return true;
	  }

	  /**
	   * 功能：出队
	   * @return 返回出队的元素
	   */
	  public String dequeue() {
	    //边界判断: 如果head == tail 表示队列为空
	    if (head == tail) return null;
	    //在头部取出一个元素
	    String ret = items[head];
	    //头指针向后移动
	    ++head;
	    //返回取出的该元素
	    return ret;
	  }

	  /**
	   * 功能:打印队列中所有的元素
	   */
	  public void printAll() {
		//通过for循环遍历所有值
	    for (int i = head; i < tail; ++i) {
	      System.out.print(items[i] + " ");
	    }
	    System.out.println();
	  }
}

```

