```javascript
/**
 * 功能:冒泡排序、插入排序、选择排序
 * @author : 小鹿
 *
 */ 

/**
 * 功能:冒泡排序
 * @param a:数组
 * @param n:数组的大小
 */
var a = [1,3,8,2,5];	
console.log(a);
var flag = false;
bubblesort(a,5);
//冒泡排序
function bubblesort(a,n){
    //如果数组长度小于等于1，返回
    if(n<=1) return;
    for(var i = 0;i < a.length;i++){
        for(var j = 0;j < n-1-i;j++){
            if(a[j]>=a[j+1]){
                var temp = a[j];
                a[j] = a[j+1];
                a[j+1] = temp;
                flag = true;
            }
        }
        if(!flag){
            break;
        }
    }
}
console.log(a);

/**
    * 功能:插入排序
    * 算法思路:取出未排序区间的数据放到value变量中，与已排序区间的数据倒序一一比较，如果要插入的数据比value大
    * 就放到该数据的后方（也就是i的位置，我们用j+1替换（j+1=i））,前边是与排序区间的最后一个数据比较，如果我们value
    * 比最后一个比较的数据要小，我们要把被比较的数据向后移动一位（a[j+1] = a[j]），指针 j 向前移动，指向下一个被比较的数据，
    * 如果满足条件，则插入到给数据的前方。
    * @param a:数组
    * @param n:数组的大小
    */
insertsort(a,5);
//插入排序
function insertsort(a,n){
    if(n<=1) return;
    for(var i = 1;i < n;i++){
        var value = a[i];
        for (var j = i-1; j >= 0; --j) {
            if (a[j] > value) {
                a[j+1] = a[j];  
            } else {
                break;
            }
        }
        a[j+1] = value; 
    }
}
```

