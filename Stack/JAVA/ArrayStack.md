```java
package easy_test;

/**
 * 功能:基于数组的顺序栈
 * 
 * @author:小鹿
 *
 */
public class ArrayStack {
	
   private String[] items;  // 数组
   private int count;       // 栈中元素个数
   private int n;           // 栈的大小

   // 初始化数组，申请一个大小为 n 的数组空间
   public ArrayStack(int n) {
     this.items = new String[n];
     this.n = n;
     this.count = 0;
   }
 
   /**
    * 功能:入栈
    * 说明:数组入栈的入口为数组尾部
    * @param item :入栈数据元素
    * @return:是否入栈成功
    */
   public boolean push(String item) {
     // 数组空间不够了，直接返回 false，入栈失败。
     if (count == n) return false;
     // 将 item 放到下标为 count 的位置
     items[count] = item;
     //数组长度+1
     ++count;
     //入栈成功
     return true;
   }
  
   /**
    * 功能:出栈
    * 
    * @return:返回出栈元素
    */
   public String pop() {
     // 栈为空，则直接返回 null
     if (count == 0) return null;
     // 返回下标为 count-1 的数组元素
     String tmp = items[count-1];
     //数组长度-1
     --count;
     //返回出栈数据元素
     return tmp;
   }
}

```

