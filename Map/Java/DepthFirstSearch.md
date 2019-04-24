```java
/**
 * 公众号:「一个不甘平凡的码农」
 * @author 小鹿
 * 功能:深度优先遍历
 * 
 */

public class DepthFirstSearch {
	
	boolean found = false; 
	private int v; 
    private LinkedList<Integer> adj[]; 

    public DepthFirstSearch(int v) {
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
    
	public void dfs(int s, int t) {
	  // 停止递归
	  found = false;
	  
	  boolean[] visited = new boolean[v];
	  int[] prev = new int[v];
	  // 初始化路径
	  for (int i = 0; i < v; ++i) {
	    prev[i] = -1;
	  }
	  
	  recurDfs(s, t, visited, prev);
	  print(prev, s, t);
	}
	/**
	 * 
	 * @param w : 起始点
	 * @param t : 终    点
	 * @param visited:记录已经访问过的点
	 * @param prev:记录起始点到终点的路径
	 */
	private void recurDfs(int w, int t, boolean[] visited, int[] prev) {
	  // 递归终止条件(找到终点，不再递归)
	  if (found == true) return;
	  // 记录起始位置
	  visited[w] = true;
	  // 判断是否找到终点
	  if (w == t) {
	    found = true;
	    return;
	  }
	  for (int i = 0; i < adj[w].size(); ++i) {
		// 取出当顶点相连接的顶点
	    int q = adj[w].get(i);
	    // 判断是否已经访问过
	    if(!visited[q]) {
	      // 存储路径
	      prev[q] = w;
          // 进行递归
	      recurDfs(q, t, visited, prev);
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

