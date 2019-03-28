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
		//递归
        const quickSort = (arr,startIndex,endIndex,k)=>{
            //判断索引值是否大于元素个数
            if (k > endIndex) {
                return -1;
            }
            //终止条件
            if(startIndex < endIndex){
               //区分点
               let pivot = endIndex;
                //获取区分点索引
                let partitionIndex = partition(arr,pivot,startIndex,endIndex);
				// 判断查找该下标存储的数是否为最大数据？
                while(partitionIndex + 1 !== k){
                    if(partitionIndex + 1 > k){
                        quickSort(arr,startIndex,partitionIndex - 1)
                    }else{
                        quickSort(arr,partitionIndex + 1,endIndex)
                    }
                }
                //返回该元素
                return arr[partitionIndex];
            }
        }

        const partition = (arr,pivot,startIndex,endIndex)=>{
            //取区分点的值
            let pivotVal = arr[pivot];
            //定义指针
            let swapIndex = startIndex;
            for(let i = startIndex; i < endIndex; i++){
                if(arr[i] > pivotVal){
                    swap(arr,i,swapIndex)
                    swapIndex++;
                }
            }
            swap(arr,swapIndex,pivot)
            return swapIndex;
        }

        const swap = (arr,i,j)=>{
            if (i === j) return;
            let temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }

        const testArr = [1,2,3,3,4]
        let i = 0
        while(i < 5){
            testArr.push(Math.floor(Math.random()*10));
            i++;
        }
        console.log(quickSort(testArr,0,testArr.length - 1,1));
        console.log("Quick:"+testArr)
```

