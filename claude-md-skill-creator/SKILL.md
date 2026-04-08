---
name: claude-md-skill-creator
description: |
  指导用户创建和优化 CLAUDE.md 配置文件。
  当用户提到 "CLAUDE.md", "claude.md", "创建 claude.md", "怎么写 CLAUDE.md", 
  "CLAUDE.md 怎么配置", "给项目添加 CLAUDE.md", "优化 CLAUDE.md" 等时触发。
  适用于任何需要为 Claude Code 项目设置持久记忆、操作边界或上下文引导的场景。
---

# CLAUDE.md Skill Creator

帮助用户创建高效的 CLAUDE.md 配置文件，让 Claude 更好理解项目。

## 核心理念

CLAUDE.md 是**配置文件**，不是项目文档。它会：
- 成为 Claude 系统提示词的一部分，优先级高于普通提示词
- 为 Claude 提供项目持久记忆
- 设定 Claude 不会打破的操作边界
- 每次会话自动加载

## 创建流程

### 步骤1：确定层级位置

询问用户 CLAUDE.md 的放置位置：

| 层级 | 位置 | 使用场景 |
|------|------|----------|
| 全局 | `~/.claude/CLAUDE.md` | 个人偏好设置、通用规则 |
| 项目 | `/project/CLAUDE.md` | 项目架构、团队规范 |
| 嵌套 | `/project/src/CLAUDE.md` | 特定目录的规则或模式 |

**monorepo 示例结构：**
```
my-monorepo/
├── CLAUDE.md              # 整个仓库的规则
├── apps/
│   ├── web/CLAUDE.md      # 前端特定规则
│   └── api/CLAUDE.md      # 后端特定规则
├── packages/
│   └── shared/CLAUDE.md   # 共享库规则
└── tests/CLAUDE.md        # 测试规范
```

### 步骤2：选择文件命名

- **CLAUDE.md** - 标准名称，提交到 git，与团队共享
- **CLAUDE.local.md** - 加入 .gitignore，用于个人偏好，不推送到仓库

### 步骤3：编写核心内容 (WHAT/WHY/HOW)

```markdown
## 关于本项目
[一句话描述项目：基于 XX 的 YY，用于 ZZ]

## 技术栈
- 框架: FastAPI / React / Vue / etc.
- 数据库: PostgreSQL / MongoDB / etc.
- ORM: SQLAlchemy / Prisma / etc.
- 主要依赖: [关键库]

## 关键目录结构
- `app/models/` — 数据库模型
- `app/api/` — 路由处理器
- `app/core/` — 配置与工具函数
- `tests/` — 测试文件

## 常用命令
```bash
# 开发服务器
uvicorn app.main:app --reload

# 运行测试
pytest tests/ -v

# 数据库迁移
alembic upgrade head
```

## 代码规范
- [命名规范]
- [分支命名]
- [Commit 规范]
```

## 内容取舍指南

### ✅ 必须包含（精简普遍适用）

- 项目简介（1-2句话）
- 技术栈
- 核心命令
- 目录架构
- 操作边界（Claude 不能做什么）

### ⚠️ 按需包含

- 命名规范
- Commit 规范
- 测试要求
- 部署流程
- 工作流步骤

### ❌ 不要写入

- API key 等敏感信息
- Linter 等详细的代码规范（Claude 可从代码获知）
- 特定功能需求
- 可通过阅读代码获知的信息
- 过长内容（超过150-200条指令效果变差）

## 进阶技巧

### 1. 索引文件模式（复杂项目）

当项目复杂时，分离详细内容：

```
project/
├── CLAUDE.md                    # 核心指令（精简）
└── agent_docs/
    ├── building_the_project.md  # 构建说明
    ├── running_tests.md         # 测试指南
    ├── code_conventions.md      # 代码规范
    ├── database_schema.md       # 数据库架构
    └── deployment_process.md    # 部署流程
```

在 CLAUDE.md 中引用：
```markdown
## 附加文档
在开始具体任务前，请阅读相关文档：
- 构建：`agent_docs/building_the_project.md`
- 测试：`agent_docs/running_tests.md`
- 数据库：`agent_docs/database_schema.md`
- 部署：`agent_docs/deployment_process.md`
```

### 2. 代码导航索引

```markdown
## 导航
我已提供索引文件帮助代码导航：
- `general_index.md` — 各模块文件说明
- `detailed_index.md` — 函数签名与文档
```

### 3. 模块化 CLAUDE.md 结构

```markdown
## 开发命令
<!-- 构建、测试、运行说明 -->

## 代码规范
<!-- 适用于整个项目的编码约定 -->

## 工作流程
<!-- 完成常见任务的步骤说明 -->

## 文件边界
<!-- Claude 可以/不可以修改的内容范围 -->

## 工具集成
<!-- MCP 服务器、自定义命令等 -->
```

### 4. 具体工作流示例

```markdown
### 新增 API 接口
1. 检查 `src/api/` 中是否已存在类似接口
2. 如需新数据类型，在 `src/schemas/` 创建 schema
3. 在合适的路由文件中实现接口
4. 在 `tests/api/` 中添加测试用例
5. 更新 API 文档
6. 提交前运行完整测试套件

### 数据库 Schema 变更
1. 描述变更内容及其必要性
2. 创建迁移文件：`alembic revision --autogenerate -m "描述"`
3. 审查自动生成的迁移文件
4. 测试迁移：`alembic upgrade head`
5. 测试回滚：`alembic downgrade -1`
6. 更新相关模型和 schema
```

### 5. 按阶段区分维护

```
project/
├── CLAUDE.md                    # 当前生效配置
└── .claude/
    ├── CLAUDE.development.md    # 开发阶段
    ├── CLAUDE.deployment.md     # 部署阶段
    └── CLAUDE.debugging.md      # 调试阶段
```

### 6. MCP 集成说明

```markdown
## MCP 集成

### Slack MCP
- 仅向 #dev-notifications 频道发送消息
- 用于部署通知和构建失败通知
- 不用于单个 PR 更新通知
- 每小时限制 10 条消息

### Database MCP
- 对生产环境只读副本拥有只读访问权限
- 仅用于数据探索，绝不可写入
- 优先使用 MCP 而非直接执行原始 SQL
```

### 7. 子代理指南

```markdown
## 子代理指南

在将任务委托给子代理时：
- 安全审查：使用全新子代理，不携带实现阶段上下文
- 代码探索：子代理应首先阅读 `general_index.md`
- 文档任务：子代理可自由访问 `docs/` 目录
```

## 重要提醒

1. **少即是多**：如果超过 100-150 条指令，说明做得太多了
2. **渐进式披露优于臃肿**：使用分层结构和索引文件
3. **持续迭代**：用 `#` 持续把新规则迭代进 CLAUDE.md
4. **Claude 会忽略不相关内容**：确保指令普遍适用，不是针对特定任务

## 示例模板

### Python/FastAPI 项目

```markdown
## 关于本项目
基于 FastAPI 的 REST API，用于用户认证和资料管理。
使用 SQLAlchemy 进行数据库操作，Pydantic 进行数据验证。

## 技术栈
- Python 3.11+
- FastAPI
- SQLAlchemy 2.0
- PostgreSQL
- Alembic (迁移)
- pytest (测试)

## 关键目录
- `app/models/` — 数据库模型
- `app/api/` — API 路由
- `app/schemas/` — Pydantic schema
- `app/core/` — 配置与工具
- `tests/` — 测试文件

## 常用命令
```bash
# 启动开发服务器
uvicorn app.main:app --reload

# 运行测试
pytest tests/ -v

# 数据库迁移
alembic revision --autogenerate -m "描述"
alembic upgrade head
```

## 代码规范
- 使用 `snake_case` 命名函数和变量
- 模型文件放在 `app/models/`
- 所有 API 端点需要对应的测试
```

### React/TypeScript 项目

```markdown
## 关于本项目
基于 React + TypeScript 的前端应用，使用 Tailwind CSS 进行样式设计。

## 技术栈
- React 18
- TypeScript
- Vite
- Tailwind CSS
- React Query (数据获取)
- Zustand (状态管理)

## 关键目录
- `src/components/` — React 组件
- `src/hooks/` — 自定义 hooks
- `src/stores/` — 状态管理
- `src/api/` — API 客户端
- `src/types/` — TypeScript 类型定义

## 常用命令
```bash
# 开发服务器
npm run dev

# 构建
npm run build

# 运行测试
npm test

# 类型检查
npm run type-check
```

## 组件规范
- 使用函数组件 + hooks
- Props 需要类型定义
- 样式优先使用 Tailwind
- 复杂组件需要 stories 文件
```

## 验证清单

创建完 CLAUDE.md 后，检查：
- [ ] 内容是否在 150-200 条指令以内？
- [ ] 是否包含项目简介、技术栈、核心命令、目录架构？
- [ ] 是否移除了敏感信息？
- [ ] 指令是否普遍适用，而非针对特定任务？
- [ ] 复杂内容是否已分离到索引文件？
