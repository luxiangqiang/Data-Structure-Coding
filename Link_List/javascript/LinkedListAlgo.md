```javascript
        /**
         * 公众号:「一个不甘平凡的码农」
         * 2019/3/24
         * 带有头结点的链表(哨兵思想)
         * 1) 单链表反转
         * 2) 链表中环的检测
         * 3) 两个有序的链表合并
         * 4) 删除链表倒数第 n 个结点
         * 5) 求链表的中间结点
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

            // 功能：单链表反转
            // 步骤:
            // 1、定义三个指针(pre=null/next/current)
            // 2、判断链表是否可反转(头节点是否为空、是否有第二个结点)
            // 3、尾指针指向第一个结点的 next
            // 4、尾指针向前移动
            // 5、当前指针(current)向后移动
            // 6、将 head 指向单转好的结点
            reverseList = () =>{
                 //声明三个指针
                let current = this.head; //当前指针指向头节点
                let pre = null;//尾指针
                let next;//指向当前指针的下一个指针

                //判断单链表是否符合反转的条件(一个结点以上)？
                if(this.head == null || this.head.next == null) return -1;
                
                //开始反转
                while(current !== null){
                    next = current.next;
                    current.next = pre;
                    pre = current;
                    current = next;
                }
                this.head = pre;
            }

            //功能:验证链表为环
            //步骤:
            // 1、定义两个指针(low、fast)
            // 2、fast 指针和下一指向不能为 null
            // 3、fast 移动二步,low 前进一步
            // 4、判断 fast 和 low 是否相等
            checkCicle = () =>{
                let fast = this.head.next;
                let low = this.head;
                while(fast !== null && fast.next !== null){
                    fast = fast.next.next;
                    low = low.next;
                    if(low === fast) return true; 
                }
                return false;
            }

            //功能：删除倒数第 K 个结点
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

            //功能:求中间结点
            //步骤:
            // 1、声明两个指针(fast、slow)
            // 2、判断 fast 的下一结点和下下结点是否为 null？
            // 3、如果满足条件,fast 前移动两位， slow 前移动一位
            // 返回 slow 就是中间结点
            findMidNode = () =>{
                let fast = this.head;
                let slow = this.head;
                while(fast.next !== null && fast.next.next !== null){
                    fast = fast.next.next;
                    slow = slow.next;
                }  
                console.log(slow)
                return slow;
            }
        }

        // 功能:两个有序链表的合并
        // 步骤:
        // 1、判断两个链表是否为 null,并将链表赋予临时变量
        // 2、声明合并链表,通过 currentNode 指向当前结点
        // 3、两个链表比较大小,数值小的添加到合并链表中,合并链表进行指针移动
        // 4、将链表剩余数据添加到合并链表后边
        const mergeSortList = (listA,listB) =>{
            //判断链表是否为空
            if(listA === null) return false;
            if(listB === null) return false;
            let a = listA;
            let b = listB;

            //声明合并链表,通过 currentNode 指向当前结点
            let resultList = undefined

            //两个链表比较大小,数值小的添加到合并链表中,合并链表进行指针移动
            if (a.data < b.data) {
                resultList = a
                a = a.next
            } else {
                resultList = b
                b = b.next
            }
            let currentNode = resultList;
            while (a !== null && b !== null) {
                if (a.data < b.data) {
                    currentNode.next = a
                    a = a.next
                } else {
                    currentNode.next = b
                    b = b.next
                }
                currentNode = currentNode.next
            } 

            // 将链表剩余数据添加到合并链表后边 
            if(a !== null){
                currentNode.next = a;
            }else{
                currentNode.next = b;
            }
            //返回合并链表
            return resultList;
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

        console.log('--------------------反转链表---------------------')
        list.reverseList()
        list.print()

        console.log('---------------------检测环----------------------')
        console.log(list.checkCicle())

        console.log('----------------删除倒数第 k 的元素---------------')
        list.removeByIndexFromEnd(2)
        list.print()

        sortedList1 = new LinkedList()
        sortedList1.insert(9, 'head')
        sortedList1.insert(8, 'head')
        sortedList1.insert(7, 'head')
        sortedList1.insert(6, 'head')
        sortedList2 = new LinkedList()
        sortedList2.insert(21, 'head')
        sortedList2.insert(20, 'head')
        sortedList2.insert(19, 'head')
        sortedList2.insert(18, 'head')
        console.log('----------------合并两个有序的链表----------------')
        let resultList = mergeSortList(sortedList1.head.next,sortedList2.head.next)
        while (resultList !== null) {
            console.log(resultList.date);
            resultList = resultList.next;
        }
```

