```javascript

/**
 * 时间:2019/3/29
 * 公众号:「一个不甘平凡的码农」
 * 循环链表的插入、查找、删除
 * 功能:
 * 1)插入数据
 * 2)查找数据
 * 3)删除数据
 * @author 小鹿
 *
 */
//定义循环链表结点
class Node{
    constructor(data){
        this.data = data;
        this.next = null;
    }
}

//构造具有一个的循环链表
class LList{
    constructor(){
        this.head = new Node("head");
        this.head.next = this.head;
    }

    //按值查找结点
    findByValue = (value)=>{
        //将头指针赋值 p 指针
        let p = this.head;
        //循环遍历查找该值的节点
        while(p.data !== value){
            p = p.next;
            //判断循环链表是否只有一个节点
            if(p === this.head) return false;
        }
        return p;
    }

    //按值插入结点
    insertByValue = (value,data)=>{
        //构造新结点
        let newNode = new Node(value);
        //先按值查找结点
        let vp = this.findByValue(data);
        //查找到该值进行插入
        newNode.next = vp.next;
        vp.next = newNode;
    }

    //按值删除结点
    deleteByValue = (value)=>{
        let p = this.head;
        let pp = null;

        //判断循环链表是否只有一个节点
        if(p.next === this.head) return false;  
        //按值查找该结点且记录该结点的前驱结点
        while(p.data !== value){
            pp = p;
            p = p.next;
        }
        //查找到该结点进行删除
        pp.next = p.next;
    }

    //遍历输出所有节点
     display = ()=>{
        let p = this.head.next;
        while(p !== this.head){
            console.log(p.data);
            p = p.next;
        }
    }
}

//测试
let clist = new LList();
console.log('-----------------------插入数据----------------')
clist.insertByValue(1,"head")
clist.insertByValue(2,"head")
clist.insertByValue(3,"head")
clist.display();
console.log('-----------------------查询数据----------------')
console.log(clist.findByValue(1).data)
console.log('-----------------------删除数据----------------')
clist.deleteByValue(3)
clist.display();
```

