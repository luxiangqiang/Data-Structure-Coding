```javascript

/**
 * 2019/3/23
 * 公众号:「一个不甘平凡的码农」
 * @author 小鹿
 * 功能：单链表的插入、删除、查找
 * 【插入】：插入到指定元素后方
 * 1、查找该元素是否存在？
 * 2、没有找到返回 -1
 * 3、找到进行创建结点并插入链表。
 * 
 * 【查找】：按值查找/按索引查找
 * 1、判断当前结点是否等于null，且是否等于给定值？
 * 2、判断是否可以找到该值？
 * 3、没有找到返回 -1；
 * 4、找到该值返回结点；
 * 
 * 【删除】：按值删除
 * 1、判断是否找到该值？
 * 2、找到记录前结点，进行删除；
 * 3、找不到直接返回-1；
 */
//定义结点
class Node{
    constructor(data){
        this.data = data;
        this.next = null;
    }
}

//定义链表
class LinkList{
    constructor(){
        //初始化头结点
        this.head = new Node('head');
    }

    //根据 value 查找结点
    findByValue = (value) =>{
        let currentNode = this.head;
        while(currentNode !== null && currentNode.data !== value){
            currentNode = currentNode.next;
        }
        //判断该结点是否找到
        console.log(currentNode)
        return currentNode === null ? -1 : currentNode;
    }

    //根据 index 查找结点
    findByIndex = (index) =>{
        let pos = 0;
        let currentNode = this.head;
        while(currentNode !== null && pos !== index){
            currentNode = currentNode.next;
            pos++;
        }
        //判断是否找到该索引
        console.log(currentNode)
        return currentNode === null ? -1 : currentNode;
    }

    //插入元素(指定元素向后插入)
    insert = (value,element) =>{
        //先查找该元素
        let currentNode = this.findByValue(element);
        //如果没有找到
        if(currentNode == -1){
            console.log("未找到插入位置!")
            return;
        }
        let newNode = new Node(value);
        newNode.next = currentNode.next;
        currentNode.next = newNode;
    }

    //根据值删除结点
    delete = (value) =>{
        let currentNode = this.head;
        let preNode = null;
        while(currentNode !== null && currentNode.data !== value){
            preNode = currentNode;
            currentNode = currentNode.next;
        }
        if(currentNode == null) return -1; 
        preNode.next = currentNode.next;
    }

     //遍历所有结点
    print = () =>{
        let currentNode = this.head
        //如果结点不为空
        while(currentNode !== null){
            console.log(currentNode.data)
            currentNode = currentNode.next;
        }
    }
}

//测试
const list = new LinkList()
list.insert('xiao','head');
list.insert('lu','xiao');
list.insert('ni','head');
list.insert('hellow','head');
list.print()
console.log('-------------删除元素------------')
list.delete('ni')
list.delete('xiao')
list.print()
console.log('-------------按值查找------------')
list.findByValue('lu')
console.log('-------------按索引查找------------')
list.print()
list.findByIndex(1)
```



