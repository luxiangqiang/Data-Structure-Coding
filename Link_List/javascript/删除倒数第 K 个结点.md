```javascript
/**
 * 2019/4/25
 * 公众号:「一个不甘平凡的码农」
 * @author 小鹿
 * 功能：删除倒数第 K 个结点
 * 
 */

//定义结点
class Node{
    constructor(data){
        this.data = data;
        this.next = null;
    }
}

//定义链表
class LinkedList{
    constructor(){
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

    //步骤：
    // 1、检测链表是否为环？
    // 2、反转单链表？
    // 3、判断是否能够找到该索引的结点？
    // 4、没有找到直接返回,找到直接{按值删除}
    // 5、删除完再进行链表反转
    removeByIndexFromEnd = (index) =>{
        // 检测是否为环
        if(this.checkCicle()) return false;
        // 单链表反转
        this.reverseList()

        let pos = 1;
        let currentNode = this.head.next;
        while(currentNode !== null && pos < index){
            currentNode = currentNode.next;
            pos ++;
        }

        if(currentNode == null){
            console.log('没有找到该索引对应的结点');
            return false;
        }else{
            //删除该结点数据
            this.delete(currentNode.data);
            //再进行链表反转
            this.reverseList();
        }
    }
}
 // 测试
const list = new LinkedList();
list.insert('1','head');
list.insert('2','1');
list.insert('3','2');
list.insert('4','3');
list.insert('5','4');
list.insert('6','5');
list.print();
console.log('----------------删除倒数第 k 的元素---------------')
list.removeByIndexFromEnd(2)
list.print()
```

