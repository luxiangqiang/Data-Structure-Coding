```javascript
/**
 * 时间:2019/3/31
 * 双链表的插入、删除
 * 功能:
 * 1)双链表的尾部插入
 * 2)双链表的按位置插入
 * 3)双链表的按位置删除
 * @author 小鹿
 *
 */

//定义结点
class Node{
    constructor(data){
        this.data = data;
        this.pre = null;
        this.next = null;
    }
}

//双向链表
class DoublyLinkedList{
    constructor(){
        this.head = null;
        //链表的长度
        this.length = 0;
        //双链表尾指针
        this.tail = null;
    }

    //添加元素到双向链表的尾部
    insertTailByValue = (value)=>{
        let newNode = new Node(value);
        let current = this.head;

        //判断当前双链表是否为 null
        if(this.head == null){
            this.head = newNode;
            this.tail = newNode;
        }else{
            //遍历找到链尾
            while(current.next !== null){
                current = current.next;
            }
            //将结点添加到尾部
            current.next = newNode;
            //新结点的前结点指向 node
            newNode.pre = current;
            //尾指针指向尾结点
            this.tail = newNode;
        }
        this.length++;
        return true;
    }

    // 添加元素到指定元素后
    // 参数一:添加的元素
    // 参数二:指定的位置
    insertDataByValue = (value,position)=>{
        let newNode = new Node(value);
        let current = this.head;
        let previous = null;
        let index = 0;

        //position 的边界条件
        if(position < 0 && position >= this.length){
            return false;
        }
        //如果是 0 索引，就插入头部
        if(position == 0){
            //新结点的尾指向头结点
            newNode.next = this.head;
            //头结点的前结点指向新结点
            this.head.pre = newNode;
            //将插入结点设置为新结点
            this.head = newNode;
        }else if(position === this.length){
            //将新结点插入尾部
            this.tail.next = newNode;
            newNode.pre = this.tail;
            this.tail = newNode;
        }else{
            while(index !== position){
                //记录插入节点的前一个节点
                previous = current;
                current = current.next;
                index++;
            }
            //绑定插入结点和后一个结点的关系
            newNode.next = current;
            current.pre = newNode;
            //绑定插入节点和前一个节点的关系
            previous.next = newNode;
            newNode.pre = previous;
        }
        this.length++;
        return true;
    }   

    // 移除双向链表中某个位置的元素
    removeByValue = (position)=>{
        let current = this.head;
        let index = 0;
        let previous = null;

        //position 的边界条件
        if(position < 0 && position >= this.length){
            return false;
        }

        // 移除链表的头部
        if(position === 0){
            this.head = current.next;
            this.head.pre = null;
        }else if(position === this.length){
            // 移除尾部结点
            current = this.tail;
            this.tail = current.pre;
            this.tail.next = null;
        }else{
            //移除中间结点元素
            while(index !== position){
                previous = current;
                current = current.next;
            }
            previous.next = current.next;
            current.next.pre = previous;
        }   
        this.length--;
        return current.data;
    }

    //打印双链表
    display = ()=>{
        let p = this.head;
        while(p !== null){
            console.log(p.data);
            p = p.next;
        }
    }
}

//测试
let list = new DoublyLinkedList();
console.log('---------------------插入数据------------------------')
list.insertTailByValue(1);
list.insertTailByValue(2);
list.insertTailByValue(3);
list.insertTailByValue(4);
list.display();
console.log('-------------------插入数据(位置)--------------------')
list.insertDataByValue(5,4);
list.insertDataByValue(6,0);
list.display();
console.log('---------------------删除数据------------------------')
list.removeByValue(0);
list.removeByValue(5);
list.display();
```

