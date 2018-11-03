```java
package easy_test;

/**
 * 功能:使用前后栈实现浏览器的前进后退。
 * @author :小鹿
 *
 */

public class SampleBrowser {
	//存储当前页面变量
    private String currentPage;
    //backStack 栈（存储浏览器前进时浏览过的页面）
    private LinkedListBasedStack backStack;
    //forwardStack 栈（存储浏览器后退时浏览过的页面）
    private LinkedListBasedStack forwardStack;
	
	//构造函数
	public SampleBrowser() {
		//新建一个浏览器栈(backStack)
        this.backStack = new LinkedListBasedStack();
        //新建一个浏览器栈(forwardStack)
        this.forwardStack = new LinkedListBasedStack();
    }
	
	//主函数
	public static void main(String[] args) {
	       SampleBrowser browser = new SampleBrowser();
	       //打开新网页
	       browser.open("http://www.baidu.com");
	       //打开新网页
	       browser.open("http://news.baidu.com/");
	       //打开新网页
	       browser.open("http://news.baidu.com/ent");
	       //后退网页
	       browser.goBack();
	       //后退网页
	       browser.goBack();
	       //前进页面
	       browser.goForward();
	       //打开新页面
	       browser.open("http://www.qq.com");
	       //前进页面
	       browser.goForward();
	       //后退网页
	       browser.goBack();
	       //前进页面
	       browser.goForward();
	       //后退网页
	       browser.goBack();
	       //后退网页
	       browser.goBack();
	       //后退网页
	       browser.goBack();
	       //后退网页
	       browser.goBack();
	       //查看当前页面
	       browser.checkCurrentPage();
	}
  
	//打开一个网页
    public void open(String url) {
    	//判断是不是第一个入栈页面(除第一次调用外，将前一个页面入栈，让当前的页面显示到浏览器)
        if (this.currentPage != null) {
        	//入栈操作
            this.backStack.push(this.currentPage);
            this.forwardStack.clear();
        }
        //第一个入栈网页，显示到界面
        showUrl(url, "Open");
    }

    //判断栈大小是否大于0
    public boolean canGoBack() {
        return this.backStack.size() > 0;
    }
    
    //判断第二个占是否存在页面
    public boolean canGoForward() {
        return this.forwardStack.size() > 0;
    }
    
    //浏览器退回
    public String goBack() {
    	//如果栈不为空
        if (this.canGoBack()) {
        	//将当前页放到另一个栈中
            this.forwardStack.push(this.currentPage);
            //原来的栈数据出栈
            String backUrl = this.backStack.pop();
            //将出栈的页面显示到浏览器界面上
            showUrl(backUrl, "Back");
            //返回该页面
            return backUrl;
        }
        //否则提示不能进行浏览器倒退
        System.out.println("* Cannot go back, no pages behind.");
        return null;
    }

    //浏览器前进
    public String goForward() {
    	//判断第二个栈中是否有页面
        if (this.canGoForward()) {
        	//当前页面入栈
            this.backStack.push(this.currentPage);
            //前进的页面出栈
            String forwardUrl = this.forwardStack.pop();
            //将出栈的页面显示到浏览器中
            showUrl(forwardUrl, "Foward");
            //返回当前页面
            return forwardUrl;
        }
        //否则，提示浏览器不能进行前进
        System.out.println("** Cannot go forward, no pages ahead.");
        return null;
    }
    
    //显示网页，并标记为当前网页
    public void showUrl(String url, String prefix) {
        this.currentPage = url;
        System.out.println(prefix + " page == " + url);
    }
    
    //当前页面是哪一个页面
    public void checkCurrentPage() {
        System.out.println("Current page is: " + this.currentPage);
    }

    /**
     * A LinkedList based Stack implementation.
     */
    public static class LinkedListBasedStack {
    	
//			测试栈代码
//	        public static void main(String[] args) {
//	            LinkedListBasedStack stack = new LinkedListBasedStack();
//	            stack.push("A");
//	            stack.push("B");
//	            stack.push("C");
//	            stack.pop();
//	            stack.push("D");
//	            stack.push("E");
//	            stack.pop();
//	            stack.push("F");
//	            stack.print();
//
////	        String data = stack.getTopData();
////	        System.out.println("Top data == " + data);
//	        }

	    //栈的大小
	    private int size;
	    //栈顶部
	    private Node top;
	    
	    //该定义一个结点类
	    public static class Node {
	    	
	    	//数据域
	        private String data;
	        //指针域
	        private Node next;
	
	        public Node(String data) {
	            this(data, null);
	        }
	
	        public Node(String data, Node next) {
	            this.data = data;
	            this.next = next;
	        }
	
	        public void setData(String data) {
	            this.data = data;
	        }
	
	        public String getData() {
	            return this.data;
	        }
	
	        public void setNext(Node next) {
	            this.next = next;
	        }
	
	        public Node getNext() {
	            return this.next;
	        }
	    }
	    
	    //创建一个结点
	    static Node createNode(String data, Node next) {
	        return new Node(data, next);
	    }
	    //清空栈
	    public void clear() {
	        this.top = null;
	        this.size = 0;
	    }
	    //入栈
	    public void push(String data) {
	        Node node = createNode(data, this.top);
	        this.top = node;
	        this.size++;
	    }
	    //出栈
	    public String pop() {
	        Node popNode = this.top;
	        if (popNode == null) {
	            System.out.println("Stack is empty.");
	            return null;
	        }
	        this.top = popNode.next;
	        if (this.size > 0) {
	            this.size--;
	        }
	        return popNode.data;
	    }
	    //获取栈顶元素
	    public String getTopData() {
	        if (this.top == null) {
	            return null;
	        }
	        return this.top.data;
	    }
	    //栈的大小
	    public int size() {
	        return this.size;
	    }
	    //输出栈中的所有元素
	    public void print() {
	        System.out.println("Print stack:");
	        Node currentNode = this.top;
	        while (currentNode != null) {
	            String data = currentNode.getData();
	            System.out.print(data + "\t");
	            currentNode = currentNode.next;
	        }
	        System.out.println();
	    }
    }
}

```

