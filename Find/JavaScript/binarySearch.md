```javascript
/**
* 公众号:「一个不甘平凡的码农」
* 2019/3/16
* 功能：最简单的二分查找
* 算法思路：
* 1、声明两个指针分别指向头和尾（low，high）
* 2、取中间数值 mid
* 3、判断是否为查找值
* 4、如果不是，移动 mid 指针,变化low,height
* 边界条件：
* 1）判断数组是否为空
* 2）两个指针的位置大小关系
* @param arr 一组数据
* @param target 查找的目标值
*/
const binarySearch = (arr,target) => {
    //如果数组没有数据，直接返回-1
    if(arr.length === 0) return -1;
    //声明两个指针分别指向头和尾（low，high）
    let low = 0
    let high = arr.length - 1;
   	//判断两个指针的位置关系
    while(low <= high){
    	//取中间值
        const mid = Math.floor((low + high) / 2);
        //判断是否为查找元素
        if(arr[mid] === target){
            return mid;
        //左移动 mid 指针
        }else if(target < arr[mid]){
            high = mid - 1;
        //右移动 mid 指针
        }else{
            low = mid + 1;
        }
    }
    return -1;
}
//测试
const arr = [1, 4, 5, 6, 7, 8, 10, 11, 23, 42, 44, 54, 56, 77, 102];
console.log(binarySearch(arr,24));


/**
* 2019/3/16
* 变体一：查找第一个值等于给定元素
* 算法思路：
* 1、如果查找到的该值等于目标元素
* 2、判断该数据前一个元素不等于给定元素当前元素就是查找的第一个值
* 3、当查找到的元素为第一个元素时，无需向前判断查找了
* 4、否则改变 high 指针向前查找
* @param arr 一组数据
* @param target 查找的目标值
*/
const binarySearch1 = (arr,target) => {
//如果数组没有数据，直接返回-1
if(arr.length === 0) return -1;
//声明两个指针分别指向头和尾（low，high）
let low = 0
let high = arr.length - 1;
while(low <= high){
    //取中间值
    const mid = Math.floor((low + high) / 2);
    if(arr[mid] === target){
            // mid 不为第一个元素且 mid 前方无相同元素
            if(mid == 0 || target != arr[mid-1]){
                return mid;
            }else{
                high = mid - 1;
            }
        }else if(target < arr[mid]){
            high = mid - 1;
        }else{
            low = mid + 1;
        }
    }
    return -1;
}
//测试
const arr = [1, 4, 5, 6, 7, 8, 10, 10, 11, 23, 23, 23, 42, 42, 44, 54, 56, 77, 102];
console.log(binarySearch1(arr,42));

/**
* 2019/3/16
* 变体二：查找最后一个值等于给定元素
* 算法思路：
* 1、如果查找到的该值等于目标元素
* 2、判断该数据后一个元素不等于给定元素当前元素就是查找的最后一个值
* 3、当查找到的元素为最后一个元素时，无需向后判断查找了
* 4、否则改变 low 指针向后查找
* @param arr 一组数据
* @param target 查找的目标值
*/
const binarySearch2 = (arr,target) => {
//如果数组没有数据，直接返回-1
if(arr.length === 0) return -1;

let low = 0
let high = arr.length - 1;
while(low <= high){
    const mid = Math.floor((low + high) / 2);
    if(arr[mid] === target){
        // mid 不为最后元素且 mid 后方无相同元素
            if(mid == arr.length-1 || target != arr[mid + 1]){
                return mid;
            }else{
                low = mid + 1;
            }
        }else if(target < arr[mid]){
            high = mid - 1;
        }else{
            low = mid + 1;
        }
    }
    return -1;
}
//测试
 const arr = [1, 4, 5, 6, 7, 8, 10, 10, 11, 23, 23, 23, 42, 42, 44, 54, 56, 77, 102];
 console.log(binarySearch2(arr,42));

/**
* 2019/3/16
* 变体三：查找第一个小于等于指定该元素的值
* 算法思路：
* 1、如果查找到的该值小于等于目标元素
* 2、如果为最后一个元素，已经达到最小，因为左边是更小的元素
* 3、如果右边的值该元素右边的值大于给定元速，说明该值就是该查找值
* 4、否则改变 low 指针向后查找
* @param arr 一组数据
* @param target 查找的目标值
*/
const binarySearch3 = (arr,target) => {
    //如果数组没有数据，直接返回-1
    if(arr.length === 0) return -1;

    let low = 0
    let high = arr.length - 1;
    while(low <= high){
        const mid = Math.floor((low + high) / 2);
        //满足条件：小于等于目标值
        if(arr[mid] <= target){
            //如果为最后一个元素，已经达到最小，因为左边是更小的元素
            //如果右边的值该元素右边的值大于给定元速，说明该值就是该查找值
            if(mid == arr.length - 1 || arr[mid + 1] > target){
                return mid;
            }else{
                //否则向右侧查找
                low = mid + 1;
            }
        }else{
            high = mid - 1;
        }
    }
    return -1;
}
//测试
const arr = [1, 4, 5, 6, 7, 8, 10, 11, 23, 42, 44, 54, 56, 77, 102];
console.log(binarySearch3(arr,12));

/**
* 2019/3/16
* 变体四：查找第一个大于等于指定该元素的值
* 算法思路：
* 1、如果查找到的该值大于等于目标元素
* 2、如果为最后一个元素，已经达到最小第一个，因为左边是更小的元素
* 3、如果右边的值该元素右边的值大于给定元速，说明该值就是该查找值
* 4、否则改变 high 指针向前查找
* @param arr 一组数据
* @param target 查找的目标值
*/
const binarySearch4 = (arr,target) => {
	//如果数组没有数据，直接返回-1
    if(arr.length === 0) return -1;

    let low = 0
    let high = arr.length - 1;
    while(low <= high){
        const mid = Math.floor((low + high) / 2);
        //如果查找到的该值大于等于目标元素
        //如果为第一个元素，是第一个最大的元素，因为右边是更大的元素
        if(arr[mid] >= target){
            if(mid == 0 || arr[mid - 1] < target){
                return mid;
            }else{
                //否则向左侧查找
                high = mid - 1;
            }
        }else{
            low = mid + 1;
        }
    }
    return -1;
}
//测试
const arr = [1, 4, 5, 6, 7, 8, 10, 11, 23, 42, 44, 54, 56, 77, 102];
console.log(binarySearch4(arr,24));
```

