# 200、岛屿数量

这道题题目是 DFS，BFS，并查集，基础题目。

本题思路，是用遇到一个没有遍历过的节点陆地，计数器就加一，然后把该节点陆地所能遍历到的陆地都标记上。

在遇到标记过的陆地节点和海洋节点的时候直接跳过。 这样计数器就是最终岛屿的数量。

那么如何把节点陆地所能遍历到的陆地都标记上呢，就可以使用 DFS，BFS或者并查集。

## DFS：

```java
import java.util.Scanner;

public class Main {
    public static int[][] dir ={{0,1},{1,0},{-1,0},{0,-1}};
    public static void dfs(boolean[][] visited,int x,int y ,int [][]grid)
    {
        for (int i = 0; i < 4; i++) {
            int nextX=x+dir[i][0];
            int nextY=y+dir[i][1];
            if(nextY<0||nextX<0||nextX>= grid.length||nextY>=grid[0].length)
                continue;
            if(!visited[nextX][nextY]&&grid[nextX][nextY]==1)
            {
                visited[nextX][nextY]=true;
                dfs(visited,nextX,nextY,grid);
            }
        }
    }
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int m= sc.nextInt();
        int n = sc.nextInt();
        int[][] grid = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                grid[i][j]=sc.nextInt();
            }
        }
        boolean[][]visited =new boolean[m][n];
        int ans = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if(!visited[i][j]&&grid[i][j]==1)
                {
                    ans++;
                    visited[i][j]=true;
                    dfs(visited,i,j,grid);
                }
            }
        }
        System.out.println(ans);
    }
}
```



## BFS：

```java
import java.util.*;

public class Main {
    public static int[][] dir = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};//下右上左逆时针遍历

    public static void bfs(int[][] grid, boolean[][] visited, int x, int y) {
        Queue<pair> queue = new LinkedList<pair>();//定义坐标队列，没有现成的pair类，在下面自定义了
        queue.add(new pair(x, y));
        visited[x][y] = true;//遇到入队直接标记为优先，
        // 否则出队时才标记的话会导致重复访问，比如下方节点会在右下顺序的时候被第二次访问入队
        while (!queue.isEmpty()) {
            int curX = queue.peek().first;
            int curY = queue.poll().second;//当前横纵坐标
            for (int i = 0; i < 4; i++) {
                //顺时针遍历新节点next，下面记录坐标
                int nextX = curX + dir[i][0];
                int nextY = curY + dir[i][1];
                if (nextX < 0 || nextX >= grid.length || nextY < 0 || nextY >= grid[0].length) {
                    continue;
                }//去除越界部分
                if (!visited[nextX][nextY] && grid[nextX][nextY] == 1) {
                    queue.add(new pair(nextX, nextY));
                    visited[nextX][nextY] = true;//逻辑同上
                }
            }
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int m = sc.nextInt();
        int n = sc.nextInt();
        int[][] grid = new int[m][n];
        boolean[][] visited = new boolean[m][n];
        int ans = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                grid[i][j] = sc.nextInt();
            }
        }
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (!visited[i][j] && grid[i][j] == 1) {
                    ans++;
                    bfs(grid, visited, i, j);
                }
            }
        }
        System.out.println(ans);
    }
}
```

bfs主要用到一个容器用来存储数据
