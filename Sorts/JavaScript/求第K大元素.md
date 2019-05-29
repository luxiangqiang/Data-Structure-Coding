```javascript
/**
 * 2019/3/28
 * 公众号: 「一个不甘平凡的码农」
 * 功能:求第 K 大数据
 * 算法思路：
 * 1）对快速排序进行改进
 * 2）快速排序返回中间值下标索引
 * 3）判断 partitionIndex + 1 是否等于 k
 * 
 * 边界条件：
 * 1）判断索引值是否大于元素个数
 * 
 * 注意:
 * 1)对于重复数据怎么做处理？
 * @author 小鹿
 */
const largestKelement = (arr,start,end,k)=>{
    // 判断 k 的范围
    if(k < 1 || k > arr.length){
        return false;
    }
    // 终止条件
    if(start > end) return;
    // 区分点
    let pivot = end;
    // 求中间下标
    let middleIndex = partition(arr,start,end,pivot);
    console.log(arr)
    if(middleIndex + 1 == k){
        console.log("第"+k+"大数据为:"+arr[middleIndex]);
        return;
    }else if(middleIndex + 1 < k){
        largestKelement(arr,middleIndex+1,end,k);
    }else{
        largestKelement(arr,start,middleIndex-1,k);
    }
}       
// 区分点
const partition = (arr,start,end,pivot)=>{
    // 存储中间点
    let pivotVal = arr[pivot];
    // 交换点
    let startIndex = start;
    // 调整数据
    for(let i = startIndex;i < end;++i){
        if(arr[i] < pivotVal){
            swap(arr,i,startIndex);
            startIndex++;
        }    
    }
    swap(arr,startIndex,pivot);
    return startIndex;
}
// 交换
const swap = (arr,x,y)=>{
    if (x === y) return;
    let temp  = arr[x];
    arr[x] = arr[y];
    arr[y] = temp;
}

// 测试
const testArr = []
let i = 0
while(i < 5){
    testArr.push(Math.floor(Math.random()*10));
    i++;
}
console.log("Quick:"+testArr)
largestKelement(testArr,0,testArr.length - 1,3);
```

