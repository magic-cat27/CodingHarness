# CodingHarness

[English](README.md) | **简体中文**

Coding Harness是我日常使用GPT进行开发时常用的Harness，核心是确保用户在使用Coding Agent时分工明确、开发高效、覆盖需求。

## 核心设计
- 以AGENTS.md为入口。AGENTS.md只负责三件事：介绍项目概况、明确角色分工与权责、路由细节文档
- 主要角色有User, Planner和Executor。权责如下：
    - User有理论上的最高权限，主要负责提出需求，使用产品。
    - Planner负责明确用户需求后写入SPEC.md, 并且将需求转化成一套可执行方案写入PLAN.md；Planner还有维护文档系统、项目状态的职责
    - Executor负责接收PLAN.md并严格按这套文档实现功能
- 文档路由是这套Harness的核心设计，好的Router设计能让Agent精准检索到目标信息。通过角色权责的明确实现文档的精准路由：如果一个细节文档所描述的不在该角色的职责范围之内，它不仅不会看到这个文档的内容，甚至不该看到这个文档的索引。
- 更多关于文档系统的设计的细节见[/docs/document/document.md](docs/document/document.md)