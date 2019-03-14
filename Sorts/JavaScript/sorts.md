```javascript
/**
 * 公众号:「一个不甘平凡的码农」
 * 功能:冒泡排序、插入排序、选择排序
 * @author : 小鹿
 */ 

/**
 * 时间:2019/3/14 
 * 功能:冒泡排序
 * @param a:数组
 * @param n:数组的大小
 * 边界条件:
 * 1) 判断数组是否有数据
 * 算法思路:
 * 1)外循环 for 需要 n 个数据 n 次冒泡
 * 2)内循环每次冒泡的比较次数，每冒泡比较次数都 -1
 * 3)冒泡优化
 */
var a = [1,3,8,2,5];	
console.log(a);
var flag = false;
bubblesort(a,5);
//冒泡排序
function bubblesort(a,n){
    //判断数组是否有数据
    if(n<=1) return;
    //外循环
    for(let i = 0;i < a.length;i++){
        //内循环
        for(let j = 0;j < n-1-i;j++){
            if(a[j]>=a[j+1]){
                //内循环
                let temp = a[j];
                a[j] = a[j+1];
                a[j+1] = temp;
                //冒泡优化
                flag = true;
            }
        }
        if(!flag){
            break;
        }
    }
}
//打印冒泡排序结果
console.log(a);

  /**
    * 时间:2019/3/14
    * 功能:插入排序
    * 边界条件:
    * 1)判断数组是否有数据
    * 算法思路:
    * 1）外循环指针指向未排序区间的第一个数据 a[1],内循环指针指向排序区间的第一个数数据 a[0]
    * 2）将未排序区间的第一个数据存储到临时变量（value），与排序区间逐个比较大小。
    * 3）如果小于排序区间的数据，已排序区间数据向后移动一位a[j+1] = a[j];否则直接break，插入到数组合适位置。
    * @param a:数组
    * @param n:数组的大小
    */
insertsort(a,5);
//插入排序
function insertsort(a,n){
    //判断数组是否有数据
    if(n<=1) return;
    //外循环（未排序区间）
    for(var i = 1;i < n;i++){
        //未排序区间第一个数据
        var value = a[i];
        //排序区间倒序遍历比较
        for (var j = i-1; j >= 0; --j) {
            if (a[j] > value) {
                a[j+1] = a[j];  
            } else {
                break;
            }
        }
        //j指针指向排序区间比临时temp数据小的数据，所以插入到该数据前方
        a[j+1] = value; 
    }
    //打印插入排序结果
    console.log(a);
}
```

