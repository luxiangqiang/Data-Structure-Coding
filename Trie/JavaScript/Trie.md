```javascript
/**
 * 时间:2019/3/30
 * 公众号：「一个不甘平凡的码农」
 * 字典树
 * 功能:
 * 1)插入数据
 * 2)查找数据
 * @author 小鹿
 *
 */
//定义树节点(数组充当节点)
class TrieNode{
    constructor(data){
        //存储字符
        this.data = data;
        //存储下一结点的指针
        this.children = new Array(26);
    }
}
//字典树
class TrieTree{
    constructor(data){
        //根节点不存储数据
        this.root = new TrieNode('/');
    }

    //插入数据
    //步骤：
    //1、遍历字符串
    //2、计算字符的下标索引
    //3、判断该下标是否存在数据进行插入
    //4、遍历下一结点
    insertByValue = (word)=>{
        let node = this.root;
        //for 循环遍历插入数据
        for(let char of word){
            //获取下标索引
            let index = char.charCodeAt() - 'a'.charCodeAt();
            //判断该下标的数据是否已存字符
            if(node.children[index] == null){
                //如果没有存放，就将该字符存入结点
                node.children[index] = new TrieNode(char);
            }
            //指向下一结点
            node = node.children[index];
        }
        return true;
    }

    //查找数据
    //步骤：
    //1、遍历字符串
    //2、计算字符串的下标索引
    //3、判断该索引的数据为 null
    //4、继续遍历
    findByValue = (word)=>{
        let node = this.root;
        //遍历单词开始查询
        for(let char of word){
            let index = char.charCodeAt() - 'a'.charCodeAt();
            //判断是否存在该字符
            if(node.children[index] == null){
                return false;
            }else{
                node = node.children[index];
            }
        }
        return true;
    }
}

//测试
const tree = new TrieTree();
let strs = ['how','hi','her','hello','so','see'];
console.log('-----------------------插入数据-----------------------')
for(let str of strs){
    tree.insertByValue(str);
}
console.log('-----------------------查找存在数据-----------------------')
for(let str of strs){
    console.log(tree.findByValue(str));
}
console.log('-----------------------查找不存在数据-----------------------')
console.log(tree.findByValue('world'));

```

