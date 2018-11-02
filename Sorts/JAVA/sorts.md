```java
package easy_test;

/**
 * 功能:冒泡排序、插入排序、选择排序
 * @author : 小鹿
 *
 */
public class Sorts {
   
   /**
    * 功能:冒泡排序
    * @param a:数组
    * @param n:数组的大小
    */
   public static void bubbleSort(int[] a, int n) {
	 //如果数组为空,结束排序
     if (n <= 1) return;

     //否则冒泡排序（外层循环是  n 个数据需要冒泡  n - 1 次）
     for (int i = 0; i <= n - 1; ++i) {
       // 提前退出标志位
       boolean flag = false;
       //内层循环是（每趟循环交换的次数，每趟的交换次数是总数据-1）
       for (int j = 0; j < n - 1 - i ; ++j) {
         if (a[j] > a[j+1]) {
           int tmp = a[j];
           a[j] = a[j+1];
           a[j+1] = tmp;
           // 此次冒泡有数据交换
           flag = true;
         }
       }
       if (!flag) break;  // 没有数据交换，提前退出
     }
   }

   /**
    * 功能:插入排序
    * 算法思路:取出未排序区间的数据放到value变量中，与已排序区间的数据倒序一一比较，如果要插入的数据比value大
    * 就放到该数据的后方（也就是i的位置，我们用j+1替换（j+1=i））,前边是与排序区间的最后一个数据比较，如果我们value
    * 比最后一个比较的数据要小，我们要把被比较的数据向后移动一位（a[j+1] = a[j]），指针 j 向前移动，指向下一个被比较的数据，
    * 如果满足条件，则插入到给数据的前方。
    * @param a:数组
    * @param n:数组的大小
    */
   public static void insertionSort(int[] a, int n) {
	 //如果数组为空,结束排序
     if (n <= 1) return;
     //否则，进行插入排序
     for (int i = 1; i < n; ++i) {
       //从下标为1的数据开始与前边元素进行比较，找到合适位置进行插入
       int value = a[i];
       //j指针下边比 i 小 1（在 i 指针的）
       int j = i - 1;
       // 查找要插入的位置并移动数据
       for (; j >= 0; --j) {
    	 //要插入数据与已排序的数据进行一一比较
         if (a[j] > value) {
           //不满足条件就进行数据向后移动，指针J指向下一个被比较数据
           a[j+1] = a[j];
          } else {
        	break;
          }
        }
       	//找到合适位置，进行插入
        a[j+1] = value;
      }
    }

	/**
	 * 功能:选择排序
	 * 算法思想:在未排序的区间里选择最小的数据元素放到已排好序的区间的末尾。
	 * @param a:要排序的数组
	 * @param n:数组的长度
	 */
	public static void selectionSort(int[] a, int n) {
	   //如果数组为空,结束排序
	   if (n <= 1) return;

//	   for (int i = 0; i < n; ++i) {
//	     // 查找最小值
//	     int minIndex = i;
//	     int minValue = a[i];
//	     for (int j = i; j < n; ++j) {
//	       if (a[j] < minValue) {
//	         minValue = a[j];
	   
	    //外循环，i 用来标记未排序区间的第一个元素，将其假设为未排序区间的最小值
	    for (int i = 0; i < n - 1; ++i) {
	      // 查找最小值
	      int minIndex = i;
	      //在未排序区间进行遍历寻找最小数据
	      for (int j = i + 1; j < n; ++j) {
	    	//与当前最小数据进行比较
	        if (a[j] < a[minIndex]) {
	          //如果比当前最小数据还要小，则将下标给 minIndex
	          minIndex = j;
	        }
	      }
	      //如果当前的 i 就是最小数据，则继续寻找下一个数据
	      if (minIndex == i) {
	        continue;
	      }
	      // 将在区间选出的最小数据放到已排好数据的末尾
	      int tmp = a[i];
	      a[i] = a[minIndex];
	      a[minIndex] = tmp;
      } 
   }
}

```

