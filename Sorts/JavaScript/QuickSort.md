```javascript
/**
 * 2019/3/15
 * 公众号: 「一个不甘平凡的码农」
 * 功能:快速排序
 * @author 小鹿
 */

/**
* 时间：2019/3/15
* 功能:递归
* 1）终止条件
* 2）选择数组最后一个数据为区分点
* 3) 根据区分点进行区分partition
* 4）左右部分数据进行递归
* @param arr    要分治的数组
* @param start	数组起始位置
* @param end    数组终止位置
*/
const quickSort = (arr,start,end) => {
    //递归终止条件
    if(left < right){

        //区分点每次选择最后元素
        let pivot = right;

        //获取区分点
        let partitionIndex = partition(arr,pivot,start,end)

        //区分点两端开始递归
        //左递归
        quickSort(arr,left,partitionIndex - 1 < start ? start : partitionIndex - 1)
        //右递归
        quickSort(arr,partitionIndex + 1 > end ? end : partitionIndex + 1,end)
    }
}

/**
* 时间：2019/3/15
* 功能:获取分区点 pivot
* @param arr     要分治的数组
* @param pivot	 区分点
* @param start   数组起始位置
* @param end     数组终止位置
*/
const partition = (arr,pivot,start,end) => {
    // 存储区分点元素
    const pivotVal = arr[pivot];
    // 大小值交换指针
    let startIndex = start;
    // 遍历数据根据 pivot 进行划分
    for(let i = start; i < end; i++){
        if(arr[i] < pivotVal){
            swap(arr,i,startIndex);
            startIndex ++;
        }
    }
    //将 pivot 点元素放入区分点位置
    swap(arr,startIndex,pivot);
    //返回已排好的区分点
    return startIndex;
} 

//交换
const swap = (arr,i,j) => {
    const temp = arr[i]
    arr[i] = arr[j]
    arr[j] = temp
}

//随机数据进行排序
const testArr = []
let i = 0
while(i < 100){
    testArr.push(Math.floor(Math.random()*1000));
    i++;
}

//快速排序测试
quickSort(testArr,0,testArr.length - 1);
console.log("Quick:"+testArr)

```

