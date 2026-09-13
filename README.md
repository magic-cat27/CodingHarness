# CodingHarness

一套基于上下文工程（Context Engineering）的 Coding Agent 协作文档框架。

CodingHarness 把人与编程智能体协作时需要的角色、规则和项目记忆组织成一套可迁移的 Markdown 文档。它是我在日常 AI 编程实践中整理的 Harness，用来明确谁做决策、智能体何时读取哪些信息，以及一次任务如何从需求走到经过检查的交付。

当前仓库提供文档模板，没有运行时程序、自动调度器或需要安装的软件包。角色切换、任务交接和文档更新需要由使用者与智能体执行；文档中的权限是协作约定，不是程序强制的访问控制。

## 设计思路

### 从一个入口按需读取

[AGENTS.md](AGENTS.md) 是文档入口，负责介绍项目、划分角色并提供路由。细节通过“触发条件 → 文件路径”逐层展开：

```text
AGENTS.md
  ├─ 当前角色 → docs-agent/role/
  ├─ 开发、验证与发布 → docs/development/development.md
  │                      └─ spec/quality.md、runtime.md、git.md
  └─ 维护文档系统 → docs/document/document.md
```

入口保持简短，具体规则放在各自负责的文档里。智能体在需要时读取对应内容，减少无关信息进入当前上下文。

### 分开决策、执行与审查

模板采用以下工作流：

```text
用户 → Planner GPT-Work → Executor GPT-Work → Codex
          需求与计划          分配与审查         具体执行
```

| 角色 | 主要职责 |
| --- | --- |
| 用户 | 确定方向、需求与验收标准，批准计划和重要外部操作。 |
| Planner GPT-Work | 把需求整理成规格与可执行计划，明确范围和待决事项。 |
| Executor GPT-Work | 把已批准的计划拆成有边界的任务，审查实际改动与验证证据。 |
| Codex | 在指定路径和范围内修改、检查并汇报结果。 |

这些是模板中的角色名称。它们描述的是协作职责；仓库本身不会自动启动或连接这些角色。

### 让不同信息有明确的归属

| 文档 | 保存什么 |
| --- | --- |
| [SPEC.md](docs-agent/SPEC.md) | 要解决的问题、需求、范围和验收条件。 |
| [PLAN.md](docs-agent/PLAN.md) | 实施策略、任务边界、验证预算与完成条件。 |
| [STATUS.md](docs-agent/STATUS.md) | 已验证的当前状态、限制与下一步。 |
| [REVIEW.md](docs-agent/REVIEW.md) | 审查发现、证据和修订要求。 |
| [MEMORY.md](docs-agent/MEMORY.md) | 用户认可的长期决策、理由与取舍。 |

需求、计划、事实、问题与长期决策分别记录，便于在任务交接或新会话中找回上下文。模板还规定了各角色对这些文件的读写职责。

## 如何接入项目

1. 将本仓库中的 `AGENTS.md`、`docs-agent/` 和 `docs/` 合并到目标项目根目录。如果目标项目已有同名文件，先检查并合并，保留原有规则。
2. 按 `AGENTS.md` 的 adoption checklist 完成项目适配。搜索 `ADOPTER: REQUIRED`，填写项目概述、真实路径、文档路由、开发约定、运行环境、验证命令和 Git 策略。
3. 为首个真实任务初始化 `SPEC.md`、`PLAN.md`、`STATUS.md`、`REVIEW.md` 和 `MEMORY.md`。模板示例与占位符不能当成已经验证的项目事实。
4. 在所用工具中让智能体读取 `AGENTS.md`，从 Planner 角色开始梳理需求。文档入口是否自动加载，取决于具体工具；必要时显式提供入口路径。
5. 审阅并批准计划后，用下面的角色标识进行交接。Executor 给 Codex 的任务应包含允许修改的路径、排除项、验收条件、检查方式和外部操作限制。

Executor 的启动标识：

```text
Role: Executor GPT-Work
```

Executor 分配给 Codex 的任务以此开头：

```text
Role: Codex
```

6. 根据实际改动与验证结果完成审查，更新状态后交付。提交、推送及其他外部操作遵循适配后的项目规则；当前模板要求推送前由用户明确远端与分支。

## 文件结构

```text
.
├── README.md
├── AGENTS.md
├── docs-agent/
│   ├── SPEC.md
│   ├── PLAN.md
│   ├── STATUS.md
│   ├── REVIEW.md
│   ├── MEMORY.md
│   └── role/
│       ├── Planner.md
│       ├── Executor.md
│       └── Codex.md
└── docs/
    ├── development/
    │   ├── development.md
    │   └── spec/
    │       ├── quality.md
    │       ├── runtime.md
    │       └── git.md
    └── document/
        └── document.md
```

## 当前范围

这份模板适合希望显式管理需求、上下文和审查过程的协作任务。小任务可以按项目实际情况简化角色与文件，不必为每次改动引入完整流程。

模板目前没有附带自动化效果评测，也不保证智能体一定遵守所有文档规则。实际使用仍需要人工审阅、工具权限控制和与项目相匹配的验证。
