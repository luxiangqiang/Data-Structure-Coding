```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>20万条数据快速定位IP地址的归属地</title>
    <style>
        div h2{
            text-align: center;
        }
        #div{
            width: 1000px;
            margin: auto;
        }
        #input{
            width: 400px;
            margin: auto;
        }
        button{
            margin-left: 10px;
        }
        #result{
            width: 400px;
            margin: auto;
        }
    </style>
</head>
<body>
    <div class="div">
        <h2>模拟20万数据快速定位IP地址的归属地</h2>
        <div id="input">
            请输入IP地址: <input id="ip" type="number" name="number"><button onclick="query">查询</button>
        </div>
        <div id="result">
            <p>查询结果为: <span style="color:red">山东省 潍坊市 电信</span></p>
        </div>
    </div>
</body>
<script type="text/javascript">

    //将 IP 地址转化为整数
    const ipInt = (ip) =>{
        //IP转成整型  
        var num = 0;  
        ip = ip.split(".");  
        num = Number(ip[0]) * 256 * 256 * 256 + Number(ip[1]) * 256 * 256 + Number(ip[2]) * 256 + Number(ip[3]);  
        num = num >>> 0;  
        return num;  
    }

    console.log('------------------将IP转化为32位整数---------------------');
    console.log(ipInt('255.255.255.255'));

    //将整数转化为 IP 地址
    const IntIp = (num) =>{
        var str;  
        var tt = new Array();  
        tt[0] = (num >>> 24) >>> 0;  
        tt[1] = ((num << 8) >>> 24) >>> 0;  
        tt[2] = (num << 16) >>> 24;  
        tt[3] = (num << 24) >>> 24;  
        str = String(tt[0]) + "." + String(tt[1]) + "." + String(tt[2]) + "." + String(tt[3]);  
        return str;  
    }

    console.log('------------------将整数转化为IP地址---------------------');
    console.log(IntIp(40213210));

    let i = 0;
    const arrIp = [];
    //随机生成 200000 条 IP 数据
    while(i < 10000){
        const number = Math.floor(Math.random()*10000000);
        arrIp.push(number);
        i++;
    }

    //对 20 万条数据进行快速排序
    // 参数一(arrIP):要排序的数组IP 参数二(start):指向起始指针 参数三(end):指向末尾指针
    const quickSort = (arr,startIndex,endIndex) =>{
        //递归终止条件
        if(startIndex < endIndex){
            //一般选择最后一个元素为区分点(下标索引)
            let pivot =  endIndex;
            //获取一组数据区分后的大于 pivot 点最后元素的索引
            let partitionIndex = partition(arr,pivot,startIndex,endIndex);
            //进行递归
            quickSort(arr,startIndex,partitionIndex-1);
            quickSort(arr,partitionIndex+1,endIndex);
        }
    }

    // 获取排好序的区分点 Index
    const partition = (arr,pivot,startIndex,endIndex) =>{
        //获取到该区分点的值
        let pivotVal = arr[pivot];
        //永远指向第一个大于 pivot 的值
        let swapIndex = startIndex;
        //进行筛选
        // i 为遍历数据指针
        for(let i = startIndex; i < endIndex; i++){
            if(arr[i] < pivotVal){
                swap(arr,i,swapIndex);
                swapIndex++;
            }
        }
        //将大于 pivot 的值和小于 pivot 的值中间点和 pivot 的值交换
        swap(arr,swapIndex,pivot)
        //返回区分点的索引
        return swapIndex;
    }
    
    //交换
    const swap = (arr,i,j) =>{
        let temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    //对 20 万数据匹配IP对属地(二分查找)
    const findIpAddress = (arr,value) =>{
        //声明两个指针
        let low = 0;
        let high = arr.length - 1;

        while(low <= high){
            //取中间值
            let mid = Math.floor((low + (high - low))/2);
            //判断中间值
            if(arr[mid] <= value){
                //进一步判断是否是小于 IP 区间的终点值
                if(mid == arr.length - 1 || arr[mid + 1] > value){
                    return mid;
                }else{
                    low = mid + 1;
                }
            }else{
                high = mid - 1;
            }
        }
        return false;
    }

    //判断该 IP 区间是否可以找到该 IP 地址
    const checkIp = (arr,ipStartIndex)=>{
        let text = document.getElementById('result')
        // 为了模拟，将 IP  地址分为三个区间
        if(arr[ipStartIndex] > 0 && arr[ipStartIndex] < 1000000){
            text.innerHTML('山东省 潍坊市 电信')
        }else if(arr[ipStartIndex] > 1000000 && arr[ipStartIndex] < 2000000){
            text.innerHTML('山东省 菏泽市 移动')
        }else if(arr[ipStartIndex] > 2000000 && arr[ipStartIndex] < 3000000){
            text.innerHTML('中国 福建省  连通')
        }else{
            text.innerHTML('没有找到该 ip 归属地！')
        }
    }

    
    console.log('------------------排序前的数据---------------------');
    console.log(arrIp.join('|'))
    console.log('------------------排序后的数据---------------------');
    quickSort(arrIp,0,arrIp.length - 1);
    console.log(arrIp)
    console.log('--------------------二分查找-----------------------');
    // console.log(findIpAddress(arrIp,20000))   
    
    let ip = document.getElementById('ip');
    let inInt = parseInt(ipInt(ip));

    //查询 IP 地址归属地
    const query = (ip) =>{
        //排序
        quickSort(arrIp,0,arrIp.length - 1);
        //查找
        findIpAddress(arrIp,ip)
        //判断
        checkIp(arr,index);
    }
    
</script>
</html>
```

