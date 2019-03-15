```javascript
/**
 * 2019/3/15
 * 公众号: 「一个不甘平凡的码农」
 * 功能:归并排序
 * @author 小鹿
 */

/**
* 时间:2019/3/15
* 功能:递归分治
* 算法思想:
* 1 将数据分治
* 2 终止条件
* 3 取中间值
* 4 递归 分解
* 5 合并
* @param arr 要分治的数组
*/
const mergeSort = (arr) => {
    //终止条件
    if(arr.length <= 1) return arr;
    
    //找中间数值(Math.floor() 返回小于或等于一个给定数字的最大整数)
    const middle = Math.floor(arr.length / 2);
    
    //分割数组
    const left = arr.slice(0,middle);
    const right = arr.slice(middle);
    
    //递归 分解 合并
    return mergeArr(mergeSort(left),mergeSort(right))
}

/**
* 时间:2019/3/15
* 功能: 合并函数
* 1）声明两个指针分别指向两个数组的第一个数据
* 2）进行比较，合并两个数组
* 3）将数组剩余数据追加到尾部
* @param left 数组分割的左部分
* @param right 数组分割的右部分
*/
const mergeArr = (left,right) => {
    let temp = [];
    let leftIndex = 0;
    let rightIndex = 0;
    
    //判断两个数组大小，插入新数组进行排序
    while(leftIndex < left.length  && rightIndex < right.length){
        if(left[leftIndex] <= right[rightIndex]){
            temp.push(left[leftIndex]);
            leftIndex++;
        }else{
            temp.push(right[rightIndex]);
            rightIndex++;
        }
    }
    //合并数组多余部分数据
    return temp.concat(left.slice(leftIndex)).concat(right.slice(rightIndex));
}

//随机数据进行排序
const testArr = []
let i = 0
while(i < 100){
    testArr.push(Math.floor(Math.random()*1000));
    i++;
}
//打印数组
const res = mergeSort(testArr);
console.log(res);
```

