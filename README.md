# OpenClaw Refactor Agent

<p align="center">
  <img src="https://img.shields.io/badge/status-production-green?style=flat-square" alt="status">
  <img src="https://img.shields.io/badge/team-20%20engineers-blue?style=flat-square" alt="team">
  <img src="https://img.shields.io/badge/daily_tokens-5M-orange?style=flat-square" alt="tokens">
  <img src="https://img.shields.io/badge/efficiency-%2B80%25-brightgreen?style=flat-square" alt="efficiency">
</p>

> 基于 OpenClaw 构建的自动化代码库重构 Agent，实现从技术债发现到修复闭环的全流程自动化。

## 项目背景

在中大型后端团队中，存量代码的技术债累积是长期困扰开发效率的核心问题。传统的人工 Code Review 和代码规范评估不仅耗时耗力，且难以保证覆盖率和一致性。我们构建了一套基于 OpenClaw 框架的 **AI Agent 自动化重构系统**，将技术债治理从"人工抽检"升级为"AI 全量扫描 + 自动修复 + 闭环验证"。

## 核心能力

| 模块 | 能力 |
|------|------|
| **技术债扫描** | 自动解析 AST，识别代码异味、反模式、过时 API 调用、架构违规 |
| **规范对标** | 实时对接最新架构规范文档，动态更新检测规则 |
| **重构 PR 生成** | 基于 LLM 语义理解，自动生成符合规范的重构代码及 PR 描述 |
| **闭环验证** | 自动运行受影响的单元测试，确保重构不引入回归 |
| **增量分析** | 基于 Git diff 增量扫描，仅处理变更范围内的技术债 |
| **报告仪表盘** | 可视化技术债趋势、修复率、Token 消耗等关键指标 |

## 技术架构

```
┌─────────────────────────────────────────────────┐
│                  OpenClaw Agent                  │
│  ┌───────────┐  ┌───────────┐  ┌──────────────┐ │
│  │ AST Parser│  │ Rule Engine│  │ PR Generator │ │
│  │ (Tree-sit)│  │ (Rego/YAML)│  │ (LLM-driven)│ │
│  └─────┬─────┘  └─────┬─────┘  └──────┬───────┘ │
│        │              │               │          │
│  ┌─────┴──────────────┴───────────────┴───────┐  │
│  │           Agent Orchestrator               │  │
│  │  (Task Queue + Context Manager + Memory)   │  │
│  └─────────────────┬─────────────────────────┘  │
│                    │                            │
│  ┌─────────────────┴─────────────────────────┐  │
│  │         Validation Pipeline               │  │
│  │  Unit Tests → Integration Tests → Report  │  │
│  └───────────────────────────────────────────┘  │
└─────────────────────────────────────────────────┘
```

## 落地数据

| 指标 | 数值 |
|------|------|
| 团队规模 | 20 人后端团队 |
| 日均 Token 消耗 | ~500 万 |
| 代码规范评估效率提升 | **80%** |
| PR 自动合并率 | 待补充 |
| 人工 Review 时间节省 | 待补充 |

## 典型工作流

```bash
# 1. 扫描目标仓库
openclaw scan --repo ./backend --rules ./rules/architecture.yaml

# 2. 生成重构 PR
openclaw refactor --debt-id DT-2024-0142 --target main

# 3. 自动验证
openclaw validate --pr 142 --test-scope affected

# 4. 查看报告
openclaw report --period weekly --format dashboard
```

## 为什么选择 OpenClaw

- **上下文感知**：支持全仓库级代码理解，而非单文件分析
- **可编排**：Agent 行为通过 YAML 配置编排，灵活适配不同团队规范
- **成本可控**：增量分析 + 智能缓存，精准控制 Token 消耗
- **安全闭环**：重构代码必须通过测试才可提交，零信任验证

## 适用场景

- 中大型团队存量代码治理
- 架构迁移（如单体→微服务、REST→GraphQL）
- 代码规范强制落地
- 技术债务可视化与追踪

## License

MIT
