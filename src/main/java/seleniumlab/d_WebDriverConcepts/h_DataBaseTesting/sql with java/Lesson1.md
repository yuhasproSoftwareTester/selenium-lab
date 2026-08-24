# Java with MySQL (JDBC)

## 1. What is JDBC?

JDBC (Java Database Connectivity) is a Java API to connect and run SQL queries on a MySQL database.

---

## 2. Maven Dependency

Add this to `pom.xml`:

```xml
<dependency>
    <groupId>com.mysql</groupId>
    <artifactId>mysql-connector-j</artifactId>
    <version>8.0.33</version>
</dependency>
```
---

## 3. JDBC URL for MySQL

```java
String url = "jdbc:mysql://localhost:3306/database_name";
```

---

## 4. Core Classes and Interfaces

| Name | Purpose |
|------|---------|
| `Connection` | Link between Java and MySQL |
| `DriverManager` | Creates the connection using URL, user, password |
| `Statement` | Runs simple SQL queries |
| `PreparedStatement` | Runs SQL with placeholders (safer, recommended) |
| `ResultSet` | Stores rows returned by SELECT |
| `SQLException` | Error thrown when database operation fails |

---

## 5. Connect to MySQL

```java
import java.sql.*;

public class ConnectMySQL {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/school";
        String user = "root";
        String password = "your_password";

        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            System.out.println("Connected to MySQL.");
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

---

### Using PreparedStatement (Recommended)

```java
String sql = "INSERT INTO students (name, marks) VALUES (?, ?)";

try (Connection conn = DriverManager.getConnection(url, user, password);
     PreparedStatement pstmt = conn.prepareStatement(sql)) {

    pstmt.setString(1, "Bob");
    pstmt.setDouble(2, 78.5);

    int rows = pstmt.executeUpdate();
    System.out.println(rows + " row inserted.");

} catch (SQLException e) {
    e.printStackTrace();
}
```

---

## 6. Read Data (SELECT)

```java
String sql = "SELECT id, name, marks FROM students";

try (Connection conn = DriverManager.getConnection(url, user, password);
     Statement stmt = conn.createStatement();
     ResultSet rs = stmt.executeQuery(sql)) {

    while (rs.next()) {
        int id = rs.getInt("id");
        String name = rs.getString("name");
        double marks = rs.getDouble("marks");

        System.out.println(id + " | " + name + " | " + marks);
    }

} catch (SQLException e) {
    e.printStackTrace();
}
```

---

## 7. ResultSet Methods

| Method | Returns |
|--------|---------|
| `rs.next()` | Moves to next row, true if row exists |
| `rs.getInt("column")` or `rs.getInt(1)` | Integer value |
| `rs.getString("column")` or `rs.getString(1)` | String value |
| `rs.getDouble("column")` | Double value |
| `rs.getBoolean("column")` | Boolean value |
| `rs.getDate("column")` | Date value |
| `rs.getTimestamp("column")` | Date and time value |

---
## 8. Common MySQL JDBC Errors

| Error | Cause | Fix |
|-------|-------|-----|
| `Communications link failure` | MySQL server is not running | Start MySQL service |
| `Access denied for user` | Wrong username or password | Check credentials |
| `Unknown database` | Database name is wrong | Create database first |
| `No suitable driver found` | Connector JAR missing | Add Maven dependency |
| `Public Key Retrieval is not allowed` | MySQL 8 caching_sha2_password | Add `allowPublicKeyRetrieval=true` to URL |
| `SSL connection error` | SSL not configured | Add `useSSL=false` to URL |

---

## 9. Best Practices

- Always use `try-with-resources` to close `Connection`, `Statement`, `ResultSet`.
- Use `PreparedStatement` for dynamic values to prevent SQL injection.
- Do not hardcode passwords; read from config or environment variables.

