# AI-Building-PromptStandard

Central governance repository for reusable AI project prompting, Agent execution, evidence reporting, and Owner decision control.

## Purpose

本仓库是跨项目通用的 Prompt Standard 中央发布仓库。

主要定义：

- AI 对话如何规划和思考
- Agent 如何调查实际环境
- Agent 如何执行任务
- Agent 如何逐步反馈
- AI 如何审查 Agent 结果
- PROJECT OWNER 何时参与重大决策
- Execution Block 如何组织
- 环境审查和 Delta Check 规则
- Skill 如何发现和按需加载
- Git 如何承担发布和反向验证

本仓库不保存具体项目业务规则。

具体项目通过 PROJECT_AI_BOOTSTRAP.md 引用中央规范。

## Authority Model

Local Authoring Source:

D:\AI Building_PromptStandard

Git Published Source:

https://github.com/ETlvein/AI-Building-PromptStandard

本地修改不等于正式发布。

只有 Git Commit 和 Git Push 成功后，才进入 Published Source。

## AI Entry Procedure

AI 访问本仓库时优先读取：

1. CURRENT_STANDARD.yaml
2. registries/STANDARD_REGISTRY.yaml
3. 当前任务需要的标准文件
4. 当前任务需要的模板

采用 Registry First 原则。

不得默认一次加载全部规范文件。

## Current Standard

PROMPT_STANDARD_V1.0

Status:

FROZEN

Owner Approval:

APPROVED

Freeze Date:

2026-09-19

该版本已经完成本地验证、Git 发布、远程反向验证和 PROJECT OWNER 最终批准。

稳定项目应锁定明确版本，不应直接依赖持续变化的 main。
## Repository Structure

<pre>
AI-Building-PromptStandard
|
|-- .gitattributes
|-- CURRENT_STANDARD.yaml
|-- README.md
|
|-- standards
|   |-- PROMPT_STANDARD_V1.0.md
|
|-- registries
|   |-- STANDARD_REGISTRY.yaml
|
|-- templates
|   |-- EXECUTION_BLOCK_TEMPLATE.md
|   |-- AGENT_REPORT_TEMPLATE.md
|   |-- PROJECT_AI_BOOTSTRAP_TEMPLATE.md
|
|-- changelog
    |-- CHANGELOG.md
</pre>

## Core Roles

AI Control Plane:

Research
Plan
Skill Resolution
Prompt Generation
Audit

Agent Execution Plane:

INSPECT
EXECUTE
REPORT

PROJECT OWNER:

负责重大决策、核心变更和最终验收。

## Public Repository Safety

本仓库为公开仓库。

禁止提交：

- Password
- Token
- API Key
- Cookie
- SSH Private Key
- Certificate Private Key
- Database Password
- Patient Data
- Customer Private Data
- Unauthorized Business Secrets
- Other Sensitive Credentials

正式 Push 前必须进行 Public Repository Safety Check。

## Skill Repository

Skill 使用独立中央仓库。

本地目录：

D:\AI Building_Skills

Prompt Standard 负责 Skill Governance。

实际 Skill 内容由独立 Skill Repository 管理。

## Version Policy

Prompt Standard 默认锁定明确版本。

稳定项目不得因为中央 main 更新而自动改变治理规则。

升级必须采用：

Explicit Standard Upgrade
