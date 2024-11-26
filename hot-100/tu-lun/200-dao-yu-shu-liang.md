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
