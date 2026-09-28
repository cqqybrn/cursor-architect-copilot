# Architecture Copilot · 敏捷架构与分块派工副驾 (Cursor Rule)

[![Cursor Rule](https://img.shields.io/badge/Cursor-Rules-blue.svg)](https://docs.cursor.com/context/rules)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

专为 **AI 协同编程时代**打造的引导式架构设计与分块派工规则（Cursor MDC Rule）。

基于 GitHub 经典架构模式（参考 `study8677/architecture-copilot`）重构升级，专为 **Opus 4.6 / Fable 顶层思考 + Gemini 3.8 / Sonnet 高速执行** 的“三明治（Sandwich）开发流”设计。

---

## 🎯 痛点与核心哲学

在 AI 辅助开发中，常见两大误区：
1. **直接让模型写全部代码**：模型缺乏全局架构视野，前后端揉杂一团，踩坑返工成本极高。
2. **用慢模型（如 Opus）敲所有代码**：成本高昂、单步响应长达 1~2 分钟、易触发长上下文超时。

### 核心解法：三明治工作流 (The Sandwich Workflow)

```
[阶段 1: 顶层把关]  首席架构师（Claude 3.7/Opus 4.6 / Fable）
                   └─ 需求收敛 + 前后端物理隔离 + API 契约锁死 + 拆解为乐高积木模块
                          │
[阶段 2: 极限狂飙]  高速执行模型（Gemini 3.8 Flash High / Claude 3.5 Sonnet）
                   └─ 按照派工单逐模块极速编码（单模块秒级交付）+ 模块化 Git 提交
                          │
[阶段 3: 深度复审]  高级模型（Opus 4.6 / Ask & Debug 模式）
                   └─ 针对红灯高危模块（并发、状态机、鉴权）进行终审验收
```

---

## 🚦 核心机制：红绿灯分块派工系统

本规则在架构定稿后，会强制为执行模型切解出独立派工单，并标注**三色风险指示灯**：

| 标识 | 风险等级 | 对应场景 | 审核与推进策略 |
| :---: | :---: | :--- | :--- |
| 🟢 | **简单 (低风险)** | 纯静态 UI、原子组件、基础工具函数 | 执行模型完成后本地运行自测，**直接 Git Commit 放行，无需唤醒高阶模型复审**。 |
| 🟡 | **核心 (中风险)** | 业务数据转换、CRUD 数据持久化、常规 API 串联 | 完成后通过单元测试即提交，多个模块完成后半程统一复查。 |
| 🔴 | **高危 (极高风险)** | 多线程/并发争抢、网络闪断长连接重连、OAuth Token 刷新流转 | ⚠️ **核心雷区**！敲完代码后**必须呼叫 Opus 启动深度审查**，确认无死锁与竞态后再继续！ |

---

## 📦 快速使用

### 1. 引入到你的项目
直接将本项目的 `.cursor/rules/architect-pipeline.mdc` 复制到你自身项目的 `.cursor/rules/` 目录下：

```bash
mkdir -p .cursor/rules
# 复制 architect-pipeline.mdc 到此目录
```

### 2. 在 Cursor 中唤醒副驾
在 Cursor 对话框（Ask / Agent 模式）中，选择 **Claude 3.7 Sonnet / Opus 4.6**，直接向它提出你的系统构想：

> *“我想要开发一个支持多账号自动轮换的代理网关服务，请使用架构副驾帮我规划。”*

副驾将自动按照六个阶段引导你收敛系统：
1. **阶段 0**：需求定位与绝对做减法（明确 MVP 边界）
2. **阶段 1**：前后端共享契约规范（TypeScript / Pydantic 契约锁死）
3. **阶段 2**：物理架构绝对隔离（前后端独立分层）
4. **阶段 3**：目录骨架与初始 Git Commit 存档指引
5. **阶段 4**：乐高积木式模块切解与三色灯风险标识
6. **阶段 5**：生成开箱即用的 Gemini 3.8 派工 Prompt 单

---

## 📂 规则文件概览

```
.cursor/
└── rules/
    └── architect-pipeline.mdc   # 架构副驾与分块派工的核心 MDC 规则
README.md                        # 使用指引与工作流说明
LICENSE                          # MIT 开源协议
```

---

## 💡 最佳实践建议

- **契约先行 (Contract-First)**：先确认接口入参、出参和 TypeScript 类型定义，绝不先堆砌业务逻辑代码。
- **物理隔离**：坚持 `/frontend` 与 `/backend` 绝对分立，禁止任何隐式循环依赖。
- **小步快跑**：每完成一个子模块就进行一次清晰命名的 Git Commit，保证任何一步失误都可一键回滚。

---

## 📄 License

本项目采用 [MIT License](LICENSE) 开源。欢迎 Star、Fork 与提 Issue！
