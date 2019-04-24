```java
/**
 * 公众号:「一个不甘平凡的码农」
 * @author 小鹿
 * 功能:广度优先遍历
 * 
 */

public class BreadthFirstTraversal { 
    private int v; 
    private LinkedList<Integer> adj[]; 

    public BreadthFirstTraversal(int v) {
      this.v = v;
      adj = new LinkedList[v];
      for (int i=0; i<v; ++i) {
        adj[i] = new LinkedList<>();
      }
    }
  
    //无向图一条边存两次
    public void addEdge(int s, int t) { 
	    adj[s].add(t);
	    adj[t].add(s);
    }
  
    // 广度优先遍历两顶点最短路径
	public void bfs(int s, int t) {
	  if (s == t) return;
	  // 记录历史结点
	  boolean[] visited = new boolean[v];
	  visited[s]=true;
	  
	  // 记录每层结点
	  Queue<Integer> queue = new LinkedList<>();
	  queue.add(s);
	  
	  // 记录搜索路径(初始化搜索路径)
	  int[] prev = new int[v];
	  for (int i = 0; i < v; ++i) {
	    prev[i] = -1;
	  }
	  // 
	  while (queue.size() != 0) {
		  //1、层访问队列出队
	  int w = queue.poll();
	  	
	  //2、循环遍历  w 相邻的顶点
	  for (int i = 0; i < adj[w].size(); ++i) {
		  //3、逐个取出相邻的结点
	  int q = adj[w].get(i);
	  //4、判断是否遍历过
	  if (!visited[q]) {
		//5、将存储路径
	    prev[q] = w;
	    //6、判断当前的顶点是否为终点
	    if (q == t) {
	      print(prev, s, t);
	      return;
	    }
	    //7、设置相邻的结点已经给访问过
	    visited[q] = true;
	    //8、加入到层级队列中
		        queue.add(q);
		     }
	      }
	   }
	}

	// 递归打印   s->t 的路径
	private void print(int[] prev, int s, int t) { 
	    if (prev[t] != -1 && t != s) {
	    	print(prev, s, prev[t]);
	    }
	    System.out.print(t + " ");
	}
}
```

