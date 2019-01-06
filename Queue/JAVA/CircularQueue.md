```java
package easy_test;

/**
 * 公众号:「一个不甘平凡的码农」
 * 功能:循环队列的实现
 * @author 小鹿
 *
 */
public class CircularQueue {
	 // 数组：items，数组大小：n
	  private String[] items;
	  private int n = 0;
	  
	  // head表示队头下标，tail表示队尾下标
	  private int head = 0;
	  private int tail = 0;

	  // 申请一个大小为capacity的数组
	  public CircularQueue(int capacity) {
	    items = new String[capacity];
	    n = capacity;
	  }

	  /**
	   * 循环队列入队
	   * @param item 循环队列数组
	   * @return 是否插入成功
	   */
	  public boolean enqueue(String item) {
	    // 判断条件:队列是否已满
	    if ((tail + 1) % n == head) return false;
	    //插入数据
	    items[tail] = item;
	    //计算下一个插入的位置
	    tail = (tail + 1) % n;
	    //返回ture
	    return true;
	  }

	  /**
	   * 循环队列出队
	   * @return 返回
	   */
	  public String dequeue() {
	    // 如果head == tail 表示队列为空
	    if (head == tail) return null;
	    //在数组头部取出该元素
	    String ret = items[head];
	    //将头指针向后移动
	    head = (head + 1) % n;
	    //返回该元素
	    return ret;
	  }

	  public void printAll() {
		//如果数组为空，返回
	    if (0 == n) return;
	    //通过for循环遍历所有值
	    for (int i = head; i % n != tail; ++i) {
	      System.out.print(items[i] + " ");
	    }
	    System.out.println();
	  }
}

```

