```javascript
/**
 * 公众号:一个不甘平凡的码农
 * 2019/3/20
 * 堆排序
 * 算法思路:
 * 1)建堆
 * 2)排序
 * 3)测试
 * Author: 小鹿
 */
class HeapSort{
    //构造函数（传入数组）
    constructor(originArray){
        this.originArray = originArray
        console.log(this.originArray)
    }

    
    /**
     * 建堆（从上到下）
     * 返回数组
     */	
    buildHeap = () =>{
        const arr = this.originArray
        const startIndex = Math.floor(arr.length)/2
		//对非叶子元素进行堆化
        for(let i = startIndex; i >= 1; i--){
            this.heapify(arr,arr.length,i)
        }
        return arr;
    }

    //堆化
    //arr:堆化的数组
    //len数组的长度
    //i 要堆化的元素
    
    /**
     * 堆化
     * arr: 堆化的数组
     * len：数组的长度
     *  i ：要堆化的元素
     */
    heapify = (arr,len,i) =>{
        while(true){
            //存储要堆化元素的下标
            let maxPos = i;
            //先比较与左子节点的大小
            if(2*i <= len && arr[i] < arr[2*i] ) maxPos = 2*i;
            //比较右子节点
            if(2*i+1 <= len && arr[maxPos] < arr[2*i+1]) maxPos = 2*i + 1;

            //如果根节点没有子节点或比两个子节点小，直接返回
            if(maxPos === i){
                break;
            }else{
                this.swap(arr,maxPos,i);
                //继续往下堆化
                i = maxPos;
            }
        }
    }

    /**
     * 堆排序
     */
    sort = () =>{
        //建堆
        const arr = this.buildHeap();
        let len = arr.length - 1;
        //排序(条件:结点大于两个)
        while(len > 1){
            this.swap(arr,1,len);
            len--;
            this.heapify(arr,len,1);
        }
        console.log(arr)
    }

    // 两个数组内元素交换
    swap = (arr,x,y) =>{
        let temp = arr[x];
        arr[x] = arr[y];
        arr[y] = temp;
    }
}

const arr = [null]
let i = 0
while (i <= 10) {
    const num = Math.floor(Math.random() * 100)
    arr.push(num)
    i++
}
const test = new HeapSort(arr);
test.sort();
```

