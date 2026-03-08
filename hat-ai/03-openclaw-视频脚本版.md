# 《OpenClaw 是什么》3-5 分钟视频脚本（架构增强版）

## 视频定位
- 时长：3-5 分钟
- 风格：通俗 + 工程感
- 核心比喻：Agent ≈ Docker，OpenClaw ≈ Kubernetes

---

## 0:00-0:20 开场钩子

【画面】
左侧：AI 聊天窗口飞快输出；右侧：任务看板一堆“失败/中断”红标。

【口播】
为什么 AI 看起来很聪明，到了真实工作里却经常“跑不完”？
因为会聊天，不等于会执行。
今天我用一个工程比喻讲清楚：
**Agent 像 Docker，OpenClaw 像 Kubernetes。**

---

## 0:20-1:00 问题定义

【画面】“单轮回答” vs “多步骤任务”对比

【口播】
真实任务不是一句问答，
而是一个链路：理解目标、拆任务、调用工具、检查结果、失败重试。

单个 Agent 可以做动作，
但多个 Agent 如何协同、如何调度、如何恢复，
这需要一个“编排层”。
这层，就是 OpenClaw 的价值。

---

## 1:00-1:55 核心解释（K8S 类比）

【画面】
“Agent=容器；OpenClaw=编排系统”示意图

【口播】
你可以这样理解：

- Agent 像容器：封装了某种能力，可以独立运行；
- OpenClaw 像 K8S：负责调度、编排、伸缩、治理。

所以 OpenClaw 不是另一个“更会写字的模型”，
而是让 AI 系统从 Demo 走向生产的基础设施。

---

## 1:55-3:10 底层架构（重点）

【画面】四层架构图依次高亮

【口播】
OpenClaw 可以拆成四层：

第一层，**控制平面**。
负责任务解析、流程编排、调度分发、策略约束。

第二层，**执行平面**。
Agent Runtime 真正执行动作，调用文件、API、数据库、模型网关。

第三层，**状态平面**。
管理上下文、长期记忆、任务状态机和 checkpoint，支持断点续跑。

第四层，**观测与治理平面**。
记录日志、链路追踪、成本和成功率，并支持人工接管。

这四层组合起来，系统才“可用、可控、可审计”。

---

## 3:10-4:05 用内容生产举例（你的场景）

【画面】任务流水线
Research Agent -> Structure Agent -> Writing Agent -> Script Agent -> QA Agent -> Human Review

【口播】
比如做一期 HAT 科普：

- Research Agent 先做资料整理；
- Structure Agent 给出文章骨架；
- Writing Agent 产出图文初稿；
- Script Agent 改成口播稿；
- QA Agent 做一致性检查；
- 最后人工终审发布。

OpenClaw 在背后做的是：
调度顺序、管理状态、失败重试、风险拦截。

---

## 4:05-4:40 HAT 价值与结尾

【画面】Human + OpenClaw + Agents 三层协作图

【口播】
这就是 HAT 的关键：
人定义目标和边界，
OpenClaw 保证流程可控，
Agent 完成具体执行。

记住一句话：
**Agent 决定“能做什么”，OpenClaw 决定“能不能稳定做成”。**

如果你想看下一期，我可以把这套架构拆成可直接套用的实战模板。

---

## 可直接上屏的关键词卡片
- Agent = 执行单元
- OpenClaw = 编排与治理
- Control Plane / Execution Plane / State Plane / Observability
- Human-in-the-loop
- 从 Demo 到 Production

## 备选标题
1. Agent 像 Docker，OpenClaw 像 K8S？3 分钟讲清
2. OpenClaw 底层架构：AI 系统如何从“会聊”到“会干活”
3. 为什么你需要的不只是 Agent，而是 Agent 编排层
