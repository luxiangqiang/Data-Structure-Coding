```javascript
const bf = (subString,patternString)=>{
    // 字符串转化为数组
    subString = [...subString];
    patternString = [...patternString];
    // 子串和模式串的长度
    let n = subString.length;
    let m = patternString.length;

    // 进行暴力匹配
    for(let i = 0;i <= n - m;++i){
        for(let j = 0,t = i;j < m;++j,++t){
            if(subString[t] == patternString[j]){
                if(j === 2){
                    return true;
                }
            }else{
                break;
            }
        }
    }
    return false;
}

// 测试
let str1 = "aabacfaabaacbaacaba";
let str2 = "aaa";
console.log(bf(str1,str2));
```

