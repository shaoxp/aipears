# OpenClaw 架构配图（GitHub 可直接渲染）

> 说明：本文件使用 **Mermaid** 语法，GitHub（仓库页面/README/Markdown预览）可直接渲染为图。你可把这些图块直接复制到公众号草稿或静态站点内容中。

---

## 1) 总体架构图（推荐主图）

```mermaid
flowchart TB
    U[用户/业务目标] --> CP

    subgraph CP[控制平面 Control Plane]
      P1[任务解析器\nGoal -> Task Graph]
      P2[编排器\nDAG/依赖管理]
      P3[调度器\n任务分发/负载均衡]
      P4[策略引擎\n权限/预算/风险策略]
      P1 --> P2 --> P3 --> P4
    end

    CP --> EP

    subgraph EP[执行平面 Execution Plane]
      E1[Agent Runtime A\n(Research)]
      E2[Agent Runtime B\n(Writing)]
      E3[Agent Runtime C\n(QA)]
      E4[Worker Pool\n并发执行]
      E5[Model Gateway\n模型路由/成本控制]
      E6[Tool Adapter\n文件/API/DB/浏览器]
      E1 --> E4
      E2 --> E4
      E3 --> E4
      E4 --> E5
      E4 --> E6
    end

    EP --> SP

    subgraph SP[状态平面 State Plane]
      S1[短期上下文\nSession Memory]
      S2[长期记忆\nVector/Knowledge Base]
      S3[任务状态机\nPending/Running/Failed/Succeeded]
      S4[Checkpoint\n断点续跑]
      S1 --- S2
      S2 --- S3
      S3 --- S4
    end

    CP -.读写状态.-> SP
    EP -.读写状态.-> SP

    subgraph OG[观测与治理 Observability & Governance]
      O1[Tracing\n链路追踪]
      O2[Metrics\n成功率/延迟/成本]
      O3[Logs/Audit\n日志与审计]
      O4[Human-in-the-loop\n人工审批/接管]
    end

    CP --> OG
    EP --> OG
    SP --> OG

    OG --> R[最终产出\n文章/脚本/API结果]
```

---

## 2) K8S 类比图（用于解释）

```mermaid
flowchart LR
    subgraph K8S_Analogy[工程类比（非1:1映射）]
      A1[Agent] --> A2[类似 Docker 容器\n封装能力、独立运行]
      B1[OpenClaw] --> B2[类似 Kubernetes\n编排/调度/治理]
    end

    A1 --> C1[执行单元]
    B1 --> C2[控制与协调]
    C1 --> D[任务完成]
    C2 --> D
```

---

## 3) 任务执行时序图（公众号+视频场景）

```mermaid
sequenceDiagram
    autonumber
    participant H as Human
    participant O as OpenClaw(Orchestrator)
    participant RA as Research Agent
    participant WA as Writing Agent
    participant SA as Script Agent
    participant QA as QA Agent
    participant ST as State Store

    H->>O: 提交目标（主题/受众/风格/约束）
    O->>ST: 初始化任务状态

    O->>RA: 子任务1：资料整理
    RA->>ST: 写入研究结果

    O->>WA: 子任务2：生成图文初稿
    WA->>ST: 写入文章草稿

    O->>SA: 子任务3：改写口播脚本
    SA->>ST: 写入视频稿

    O->>QA: 子任务4：一致性与风险检查
    QA->>ST: 写入质检报告

    alt 通过
      O->>H: 提交终稿待发布
    else 不通过
      O->>WA: 触发返工/重试
      WA->>ST: 更新草稿版本
      O->>H: 人工复核关键段落
    end
```

---

## 4) 从 Demo 到 Production 的能力阶梯图

```mermaid
flowchart LR
    D1[单轮问答 Demo] --> D2[单Agent自动化]
    D2 --> D3[多Agent协作]
    D3 --> D4[有状态与可恢复]
    D4 --> D5[可观测与可审计]
    D5 --> D6[人机协同生产级系统]
```

---

## 5) 你可以直接放到文章里的配图说明（可复制）

- 图1（主图）：OpenClaw 四平面架构（控制/执行/状态/治理）
- 图2（解释图）：Agent≈Docker，OpenClaw≈K8S（工程类比）
- 图3（流程图）：HAT 内容生产任务时序
- 图4（演进图）：从 Demo 到 Production

---

## 6) GitHub 发布小提示

1. 在 `.md` 中保留 ```mermaid 代码块即可。
2. GitHub 仓库页面可直接渲染 Mermaid。
3. 若你使用 GitHub Pages 的静态站点生成器，确保主题/渲染链支持 Mermaid（如 MkDocs Material、Docusaurus、部分 Jekyll 插件方案）。

---

## 7) 可选：文中引用语句

> Agent 决定“能做什么”，OpenClaw 决定“能不能稳定做成”。

> 真正的生产级 AI，不是模型堆料，而是编排、状态与治理能力的系统化。
