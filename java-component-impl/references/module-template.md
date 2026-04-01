# 模块模板参考

## pom.xml 模板

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>com.richal.learn</groupId>
        <artifactId>hand-roll</artifactId>
        <version>1.0-SNAPSHOT</version>
    </parent>

    <artifactId>[module-name]</artifactId>

    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-api</artifactId>
            <version>5.8.2</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-engine</artifactId>
            <version>5.8.2</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```

## 测试类模板

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class MyComponentTest {

    @Test
    public void testBasicOperation() {
        // Arrange
        MyComponent<String> component = new MyComponent<>();

        // Act
        component.add("test");

        // Assert
        assertEquals(1, component.size());
    }

    @Test
    public void testBoundaryCondition() {
        // 测试边界条件
    }

    @Test
    public void testException() {
        // 测试异常情况
        assertThrows(IndexOutOfBoundsException.class, () -> {
            // 触发异常的代码
        });
    }
}
```

## 主类模板

```java
package com.richal.learn;

/**
 * [组件名称] - [功能描述]
 *
 * 核心功能：
 * 1. 功能点 1
 * 2. 功能点 2
 *
 * 时间复杂度：
 * - 方法A: O(1)
 * - 方法B: O(n)
 *
 * 空间复杂度：O(n)
 *
 * @param <E> 元素类型
 */
public class MyComponent<E> {

    // --- 核心字段 ---

    /**
     * 底层数据结构
     */
    private Object[] data;

    /**
     * 元素数量
     */
    private int size;

    // --- 构造方法 ---

    public MyComponent() {
        this.data = new Object[10];
        this.size = 0;
    }

    // --- 核心方法 ---

    /**
     * 添加元素
     * @param element 要添加的元素
     */
    public void add(E element) {
        // 实现逻辑
    }

    /**
     * 获取元素
     * @param index 索引
     * @return 元素值
     */
    @SuppressWarnings("unchecked")
    public E get(int index) {
        if (index < 0 || index >= size) {
            throw new IndexOutOfBoundsException();
        }
        return (E) data[index];
    }

    /**
     * 获取大小
     * @return 元素数量
     */
    public int size() {
        return size;
    }
}
```
