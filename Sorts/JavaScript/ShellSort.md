```javascript
/**
 * 2019/5/27
 * 公众号: 「一个不甘平凡的码农」
 * 功能:希尔排序
 * @author 小鹿
 */
function shellSort(arr) {
    // 数组的总长度
    let len =arr.length;
    // 初始步长为长度的一半
    gap = Math.floor(len/2);
    // 如果步长为正整数,开始排序
    while(gap !== 0){
        // 外循环 i 控制步长
        for(let i = gap;i < len;i++){
            // 插入排序准备分组比较
            let temp = arr[i];
            // 步长比较的另一方
            let j = i - gap;
            // 如果后边小,则插入排序交换位置
            for(;j >= 0 && temp < arr[j];j -= gap){
                // 将大的数据移动到后边
                arr[j + gap] = arr[j];
            }
            // 小数据补充上去(注意:上方执行了j -= gap)
            arr[j + gap] = temp;
        }
        // 进一步缩小步长
        gap=Math.floor(gap/2);
    }
    return arr;
}

// example
let arr = [8,5,6,1,7,3,2,4];
console.log(shellSort(arr));
```

