```java
package easy_test;

/**
 * 1) 单链表反转
 * 2) 链表中环的检测
 * 3) 两个有序的链表合并
 * 4) 删除链表倒数第n个结点
 * 5) 求链表的中间结点
 *
 * Author: 小鹿
 */
public class LinkedListAlgo {
	
    /**
	 * 功能：定义 Node 结点，Node 包含数据域和引用（作用：存储所指向对象的内存地址）
	 * @author Boy Baby
	 *
	 */
   public static class Node {
      //数据域
      private int data;
      //引用（存储所指向对象的内存地址）
      private Node next;
      //构造函数（初始化数据）
      public Node(int data, Node next) {
          this.data = data;
          this.next = next;
      }
      //获取结点数据元素
      public int getData() {
          return data;
      }
  }
  //生成一个新的结点	  
  public static Node createNode(int value) {
	    return new Node(value, null);
  }

  /**
   * 功能:单链表反转
   * 思路:创建一个头指针和尾指针,现将第一个结点拿出，放到做后一个节点，并将最后一个指针的值赋值给在链表中拿出的结点并向前移动指向刚拿出的结点地址。
   * 如果还存在没有遍历完的结点，头指针就向后移动，继续遍历。
   * @param list:传入要反转的链表
   * @return
   */
  public static Node reverse(Node list) {
	//定义头结点
    Node headNode = null;
    //定义尾指针
    Node previousNode = null;
    //定义头指针并指向链表
    Node currentNode = list;
    //如果指针指向的链表不为空,就执行以下循环
    while (currentNode != null) {
      //先将指针指向的结点中存储的下一结点地址存储到 nextNode 中
      Node nextNode = currentNode.next;
      //判断指针指向该结点后是否还有结点，如果是 null 的话，就相当于指针处于链表的最后一个结点，而该结点的next是null(相当于为没有下一结点)
      if (nextNode == null) {
    	//如果是最后一个结点，拿出来当做反转链表的头结点
        headNode = currentNode;
      }
      //将已经反转好的链表地址存储到在单链表中拆解下来的结点的地址域中
      currentNode.next = previousNode;
      //尾指针向前移动一个结点
      previousNode = currentNode;
      //头指针向后移动
      currentNode = nextNode;
    }
    return headNode;
  }

  /**
   * 功能:检测单链表是否为环
   * 思路:定义两个指针(快指针、慢指针),两个指针的初始化位置是fast指针在前，slow指针在后,每判断一个两个指针是否在同一个位置来检测环，如果不在同一位置
   * 就使fast指针向后走三步，慢指针向前走一步，每走一步就判断一下。如果指针遇到 null 的情况下，就说明单链表不为null。否则这样一直循环下去，
   * 直到两个指针重合。
   * @param list:传入要检测的单链表
   * @return
   */
  public static boolean checkCircle(Node list) {
	// 如果单链表为空,直接返回false
    if (list == null) return false;
    //定义一个快指针 fast
    Node fast = list.next;
    //定义一个慢指针  slow
    Node slow = list;
    //判断两个指针指向的结点是否为空
    while (fast != null && fast.next != null) {
      //如果不为空就 fast 指针向后移动两个结点
      fast = fast.next.next;
      // solw 向后移动一个结点
      slow = slow.next;
      //如果两个指针重合,则返回 true
      if (slow == fast) return true;
    }
    //如果两个指针初始化就为 null,直接返回 false
    return false;
  }

  /**
   * 功能:单链表的合并
   * @param la:链表 la
   * @param lb:链表 lb
   * @return
   */
  public static Node mergeSortedLists(Node la, Node lb) {
	//判断两个单链表是否为null
    if (la == null) return lb;
    if (lb == null) return la;
    //分别将两个链表赋值给 p、q
    Node p = la;
    Node q = lb;
    //定义一个头结点
    Node head;
    //比较两个结点数据域中元素的大小
    if (p.data < q.data) {
      //如果  p 数据小于 q 数据，将 p 结点赋值给head
      head = p;
      //数据小的那条链表的指针向后移动一位
      p = p.next;
    } else {
      //否则，移动另一个指针
      head = q;
      q = q.next;
    }
    //将 head 结点赋值给 r
    Node r = head;
    //判断两个链表指针指到最后一个结点,要想跳出循环，肯定p、q其中有一个先遍历完
    while (p != null && q != null) {
      //如果没有指到最后的结点,继续进行比较大小
      if (p.data < q.data) {
    	//r 继承着 head 继续向下添加结点
        r.next = p;
        p = p.next;
      } else {
        r.next = q;
        q = q.next;
      }
      //r 指针向下移动，指向新添加的结点
      r = r.next;
    }
    //判断  p、q 两个链表哪一个先遍历晚，最后将剩余的链表拼接到合成链表的最后
    if (p != null) {
      r.next = p;
    } else {
      r.next = q;
    }
    //返回头结点
    return head;
  }

  /**
   * 功能:删除倒数第K个结点
   * 思路:我们想需要定义一个头指针，从链表的头部向后移动 k个单位，然后用头指针(fast)标记，在单链表的头部再定义一个指针(slow)
   * 之后，fast每向后移动一个结点，solw就紧跟移动一个结点，直到 fast 指针移动到了最后一个结点，slow 指针所指向的结点就是倒数
   * 第k个结点,进行单链表的删除即可。
   * @param list:要删除的单链表
   * @param k:倒数第 k 个
   * @return
   */
  public static Node deleteLastKth(Node list, int k) {
	//将fast指针指向list单链表的开始的第一个结点
    Node fast = list;
    //i 用来进行计数
    int i = 1;
    //通过 while 循环,正想找到第 K 个结点(这里有两个判断条件,fast != null 条件的作用是要删除倒数第k个结点
    //的单链表不能小于k的长度)
    while (fast != null && i < k) {
      fast = fast.next;
      ++i;
    }
    //如果单链表的长度小于 k ,就返回 list 单链表
    if (fast == null) return list;
    
    //前边找到第  k 个结点之后,让 slow 指向第一个结点
    Node slow = list;
    Node prev = null;
    //判断fast指针也就是最前边的指针下一个节点是否为 null(如果为null相当于到尾部了)
    while (fast.next != null) {
      //如果不为 null , fast 指针向后移动一个指针，slow 指针也要移动一个
      fast = fast.next;
      //prev 指向移动前的结点，为了区别下方单链表的长度和 k 相等
      prev = slow;
      //slow 向后移动一个
      slow = slow.next;
    }
    //这个判断是，如果单链表的长度正好等于 k ,删除倒数第K个结点也就是删除头结点。
    if (prev == null) {
      list = list.next;
    } else {
      //不为上述情况就可以用单链表的删除思想了
      prev.next = prev.next.next;
    }
    //返回已经删除结点的链表
    return list;
  }

  /**
   * 功能:求中间结点
   * 思路:定义一个指针 fast 用来移动做逻辑判断(画一下图就很清晰)
   * @param list:传入要求中间结点的链表
   * @return
   */
  public static Node findMiddleNode(Node list) {
	//如果单链表为 null,就返回 null
    if (list == null) return null;
    //slow 指向的就是 fast.next 与 fast.next.next 中间的那个结点
    Node fast = list;
    Node slow = list;
    //循环遍历满足fast指针条件单链表
    while (fast.next != null && fast.next.next != null) {
      fast = fast.next.next;
      slow = slow.next;
    }
    //返回的slow就是中间结点
    return slow;
  }
  //输入链表的所有值
  public static void printAll(Node list) {
    Node p = list;
    while (p != null) {
      System.out.print(p.data + " ");
      p = p.next;
    }
    System.out.println();
  }
}

```

