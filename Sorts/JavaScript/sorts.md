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
var flag = false;
const bubblesort = (a) =>{
    if(a.length < 1) return;
    for(let i = 0;i < a.length;i++){
        for(let j = 0;j < a.length-1-i;j++){
            if(a[j]>=a[j+1]){
                let temp = a[j];
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
//插入排序
const insertsort = (a) => {
    if(a.length <= 1) return;
    for(let i = 1;i < a.length;i++){
        let value = a[i];
        for (var j = i-1; j >= 0; --j) {
            if (a[j] > value) {
                a[j+1] = a[j];  // 数据移动
            } else {
                break;
            }
        }
        a[j+1] = value; // 插入数据
    }
}


 /**
    * 时间:2019/3/15
    * 功能:选择排序
    * 边界条件:
    * 1)判断数组是否有数据
    * 算法思路:
    * 1）外循环 0 -> n-1 设定最小数据
    * 2）内循环 i+1->n 范围数据作比较选出最小数据
    * 3）如果当前最小，则继续循环
    * 4）做交换
    * @param a:数组
    * @param n:数组的大小
    */
const selectSort = (a) => {
    //如果数组为空,结束排序
    if (a.length <= 1) return;
    //外循环，i 用来标记未排序区间的第一个元素，将其假设为未排序区间的最小值
    for(var i = 0; i < a.length-1; i++){
        var minIndex = i;
        for(var j = i+1;j < a.length;j++){
            if(a[j] < a[minIndex]){
                minIndex = j;
            }
        }
        if(minIndex == i){
            continue;
        }
        var temp = a[i];
        a[i] = a[minIndex];
        a[minIndex] = temp;
    }
}

//测试
//冒泡排序
var a = [2,5,8,1,3,9];
bubblesort(a);
console.log(a);
//插入排序
var a = [6,9,3,0,1,8]
insertsort(a);
console.log(a);
//选择排序
var a = [12,5,3,16,5];
selectSort(a);
console.log(a);
```

