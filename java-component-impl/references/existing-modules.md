# 项目现有模块速查

## 模块列表

| 模块 | Java 版本 | 主要依赖 | 代码风格参考 |
|-----|----------|---------|-------------|
| thread-pool | 1.8 | 无 | 并发工具、CAS 操作 |
| hashmap | 17 | JUnit 5 | 数据结构、扩容策略 |
| list | 23 | JUnit 5 | 数据结构、迭代器 |
| aqs-lock | 1.8 | JUnit 4 | 锁实现、队列 |
| proxy_module | 8 | 无 | 动态代理、反射 |
| spring-mini | 23 | Tomcat, FastJSON | IOC 容器、注解 |
| design-patterns | - | JUnit 5 | 设计模式实现 |

## 代码风格示例

### 数据结构风格 (参考 list 模块)

```java
/**
 * 自定义ArrayList实现，基于数组实现的动态列表
 * 提供了基本列表操作功能，包括添加、删除、获取元素等
 * @param <E> 列表中存储的元素类型
 */
public class MyArrayList<E> implements List<E> {

    /**
     * 底层存储数据的数组，初始容量为10
     */
    Object[] table = new Object[10];

    /**
     * 列表中实际元素的数量
     */
    private int size;

    /**
     * 在列表末尾添加元素
     * 时间复杂度：平均O(1)，最坏O(n)当需要扩容时
     * @param element 要添加的元素
     */
    @Override
    public void add(E element) {
        if (size == table.length) {
            resize();
        }
        table[size++] = element;
    }
}
```

### 并发工具风格 (参考 thread-pool 模块)

```java
/**
 * 自定义线程池
 */
public class MyThreadPool {

    // --- 线程池核心参数 ---
    private final int corePoolSize;
    private final int maximumPoolSize;

    // --- 内部状态 ---
    /**
     * 用于存放工作线程的集合
     */
    private final HashSet<Worker> workers = new HashSet<>();

    /**
     * 原子地记录当前工作线程的数量
     */
    private final AtomicInteger workerCount = new AtomicInteger(0);
}
```

### 注释规范

1. **类注释**：说明功能 + 核心特性 + 时间复杂度
2. **字段注释**：说明用途
3. **方法注释**：说明功能 + 时间复杂度 + 参数 + 返回值
4. **关键逻辑**：添加行内注释

### 测试风格

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class ArrayListTest {

    @Test
    public void operateTest() {
        MyArrayList myArrayList = new MyArrayList();
        for (int i = 0; i < 30; i++) {
            myArrayList.add(i);
        }
        assertEquals(30, myArrayList.size());

        myArrayList.remove(0);
        assertEquals(28, myArrayList.size());
    }
}
```

## 关键设计模式

### 扩容策略
- HashMap: 0.75 负载因子
- ArrayList: 翻倍扩容

### 并发控制
- AtomicInteger / AtomicReference
- CAS 操作
- synchronized 块

### 生命周期管理
- 构造 -> 初始化 -> 使用 -> 销毁
- 状态机设计

## 项目路径

- 项目根目录: `/Users/richal/Java/HandMade/hand-roll`
- 包名: `com.richal.learn`
- 测试包: 无包名（在 src/test/java 根目录）
