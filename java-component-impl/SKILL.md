---
name: java-component-impl
description: 辅助实现 Java 手写组件（数据结构、并发工具、设计模式等）。当用户说"帮我实现一个"、"手写一个"、"实现一个类似于"Java 组件时触发。支持创建新模块、添加测试用例、保持代码风格一致。
---

# Java 手写组件实现助手

## 触发条件

当用户请求以下内容时自动激活：
- "帮我实现一个 [组件名]"
- "手写一个 [数据结构/并发工具]"
- "实现一个类似 [JDK 类] 的版本"
- "给 hand-roll 项目添加 [功能]"

## 核心职责

1. **理解需求** - 分析用户想实现什么组件，确定复杂度和模块归属
2. **参考现有代码** - 保持项目代码风格一致（注释风格、命名规范、目录结构）
3. **设计实现方案** - 接口定义、核心数据结构、关键方法
4. **生成测试用例** - 参考 JUnit 5 风格编写测试
5. **提供文档** - 添加类注释、方法注释、时间复杂度说明

## 工作流程

### 步骤 1：需求分析

先问清楚：
- 组件类型（数据结构/并发工具/设计模式）
- 是否需要线程安全
- 是否需要支持泛型
- 性能要求

### 步骤 2：定位参考代码

在 `/Users/richal/Java/HandMade/hand-roll` 目录下查找：
- 类似实现的模块
- 对应的测试用例风格
- pom.xml 依赖配置

### 步骤 3：实现组件

遵循项目代码规范：
```java
/**
 * [组件名称] - [一句话说明]
 *
 * 核心功能：
 * - 功能点 1
 * - 功能点 2
 *
 * 时间复杂度：
 * - 方法 A: O(?)
 * - 方法 B: O(?)
 *
 * @param <E> 元素类型
 */
public class MyComponent<E> {
    // 实现
}
```

### 步骤 4：生成测试

参考项目测试风格：
```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class MyComponentTest {
    @Test
    public void testBasicOperation() {
        // 测试代码
    }
}
```

## 代码风格规范

### 注释风格
- 类注释：说明功能、核心特性、时间复杂度
- 方法注释：说明用途、参数、返回值、时间复杂度
- 关键逻辑：添加行内注释说明设计意图

### 命名规范
- 类名：`My[原类名]` 如 `MyArrayList`、`MyHashMap`
- 接口名：简洁明了 如 `List`、`RejectHandle`
- 变量名：有意义的英文单词

### 目录结构
```
[module-name]/
├── pom.xml
├── src/main/java/com/richal/learn/
│   ├── MyComponent.java
│   └── RelatedInterface.java
└── src/test/java/
    └── MyComponentTest.java
```

## 常见组件模板

### 数据结构类

需要考虑：
- 底层存储结构（数组/链表/树）
- 扩容策略
- 时间复杂度
- 是否支持泛型

### 并发工具类

需要考虑：
- 线程安全机制（锁/CAS/synchronized）
- 状态管理（Atomic 变量）
- 生命周期控制
- 拒绝/异常处理策略

### 设计模式类

需要考虑：
- 角色划分（接口/实现/客户端）
- 扩展性设计
- 使用场景示例

## 错误处理

### 实现过程中遇到问题

1. **需求不明确** - 向用户确认细节
2. **复杂度过高** - 建议分阶段实现
3. **缺少依赖** - 提供 pom.xml 配置

### 测试失败时

1. 分析失败原因
2. 检查边界条件
3. 修复实现代码
4. 补充测试用例

## 完成标准

实现完成时应满足：
- [ ] 核心功能完整实现
- [ ] 添加完整注释（类、方法、关键逻辑）
- [ ] 测试用例通过
- [ ] 代码风格与项目一致
- [ ] 时间复杂度说明清晰

## 示例对话

**用户**: 帮我实现一个阻塞队列

**响应**:
1. 确认需求：容量大小、公平/非公平、泛型支持
2. 创建模块：`blocking-queue`
3. 实现类：
   ```java
   public class MyBlockingQueue<E> {
       private final Object[] items;
       private final ReentrantLock lock;
       private final Condition notEmpty;
       private final Condition notFull;
       // ...
   }
   ```
4. 添加测试
5. 配置 pom.xml

---

**重要提醒**：
- 始终在 `/Users/richal/Java/HandMade/hand-roll` 目录下工作
- 参考 `list`、`hashmap`、`thread-pool` 模块的代码风格
- 使用 JUnit 5 编写测试
- Java 版本根据模块需求选择（参考现有模块配置）
