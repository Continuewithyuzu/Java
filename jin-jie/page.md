# Page

## **JDBC 常用类**

### **Connection 类**

`Connection` 是用于管理与数据库的连接对象，提供了与数据库交互的基础功能。

#### **核心方法**

1. **`createStatement()`**
   * 创建一个 `Statement` 对象，用于执行静态 SQL 语句。
   * 示例：`Statement stmt = conn.createStatement();`
2. **`prepareStatement(String sql)`**
   * 创建一个 `PreparedStatement` 对象，用于执行预编译的 SQL 语句。
   * 示例：`PreparedStatement pstmt = conn.prepareStatement("SELECT * FROM users WHERE id = ?");`
3. **`setAutoCommit(boolean autoCommit)`**
   * 设置是否自动提交事务。
   * 示例：`conn.setAutoCommit(false);`
4. **`commit()`**
   * 提交当前事务。
   * 示例：`conn.commit();`
5. **`rollback()`**
   * 回滚当前事务。
   * 示例：`conn.rollback();`
6. **`close()`**
   * 关闭连接并释放资源。

***

### &#x20;**Statement 类**

`Statement` 是用于执行静态 SQL 查询的对象。

#### **核心方法**

1. **`executeQuery(String sql)`**
   * 执行 `SELECT` 查询，返回一个 `ResultSet` 对象。
   *   示例：

       ```java
       Statement stmt = conn.createStatement();
       ResultSet rs = stmt.executeQuery("SELECT * FROM users");
       ```
2. **`executeUpdate(String sql)`**
   * 执行 `INSERT`、`UPDATE`、`DELETE`，返回受影响的行数。
   *   示例：

       ```java
       int rowsAffected = stmt.executeUpdate("UPDATE users SET name = 'John' WHERE id = 1");
       ```
3. **`execute(String sql)`**
   * 执行任意 SQL 语句，返回布尔值，表示结果是否为 `ResultSet`。
   *   示例：

       ```java
       boolean isResultSet = stmt.execute("SELECT * FROM users");
       ```
4. **`close()`**
   * 关闭 `Statement` 对象，释放资源。
