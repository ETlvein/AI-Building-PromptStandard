# Prompt Standard V1.0

Status: DRAFT

## 1. Purpose

本规范是跨项目通用的 AI 提示词治理标准。

目标不是规定某一个具体项目如何开发，而是统一规定：

- AI 对话如何进行规划与思考
- Agent 如何调查真实电脑环境
- Agent 如何执行任务
- Agent 如何反馈执行证据
- AI 如何审查反馈
- PROJECT OWNER 在什么情况下进行最终决策
- Prompt Standard 与 Skill 如何被不同项目复用
- Git 如何承担发布与双向验证职责

---

## 2. Core Architecture

整个体系划分为四个平面：

### AI Control Plane

AI 对话负责：

- 理解 Owner 目标
- 读取项目规则
- 研究技术路线
- 必要时搜索 Web、GitHub、官方文档和已有开源项目
- 查询 Prompt Standard
- 查询 Skill Registry
- 选择需要的 Skill
- 进行方案设计
- 拆分 Execution Block
- 生成 Agent Prompt
- 审查 Agent 反馈
- 判断是否继续、阻断或提交 Owner 决策

AI 不假装知道本地电脑的真实状态。

### Agent Execution Plane

Agent 固定承担三个主要职责：

INSPECT → EXECUTE → REPORT

即：

1. 调查实际环境
2. 按授权执行
3. 返回真实执行证据

Agent 不负责替 PROJECT OWNER 决定项目方向。

Agent 不得自行扩大需求或改变已批准的核心设计。

### Evidence Plane

Agent 的执行结果必须通过结构化证据反馈。

禁止仅回复：

- 已完成
- 已修复
- 测试通过

必须提供能够供 AI 与 Owner 判断的执行证据。

### Owner Decision Authority

PROJECT OWNER 保留最终决策权。

Owner 主要处理：

- 核心需求变化
- 架构变化
- Breaking Change
- 高风险数据操作
- 重大数据库迁移
- 安全策略变化
- 项目阶段里程碑
- 最终产品验收
- AI 无法自行解决的重大冲突

Owner 不需要审批每一个普通施工步骤。

---

## 3. Default Project Flow

默认顶层流程：

OWNER GOAL
→ AI RESEARCH / PLAN
→ AGENT EXECUTION BLOCK
→ AGENT REPORT
→ AI AUDIT
→ CONDITIONAL GATE
→ NEXT BLOCK

不得把每一个细小操作都变成独立 Owner Gate。

---

## 4. Execution Block

项目施工以 Execution Block 为主要执行单位。

一个 Execution Block：

- 应具有一个明确目标
- 可以包含多个 Atomic Step
- 应能够独立验证
- 不应无边界扩张

推荐：

一个 Block 包含若干连续的小步骤，例如：

- 创建目录
- 创建配置
- 创建基础文件
- 修改代码
- 执行测试
- 回归验证

Atomic Step 应有反馈，但不等于每一步都要求 Owner 审批。

---

## 5. Agent Step Feedback

Agent 每一个实际执行步骤都必须输出最小状态反馈，例如：

STEP
ACTION
STATUS
RESULT

推荐状态：

PASS
FAIL
SKIPPED
BLOCKED

Block 结束后必须提供 Block Report。

---

## 6. Environment Inspection

环境审查采用：

Block-Level Preflight

而不是：

Every-Step Full Environment Review

即：

进入一个新的 Execution Block 前，只检查该区块真正相关的环境。

例如：

- Node 任务检查 Node
- PostgreSQL 任务检查数据库
- Docker 任务检查 Docker
- Firefox 插件任务检查插件运行环境

不得无意义地每一步重新扫描整个电脑环境。

---

## 7. Delta Check

如果任务执行已经产生了预期变化，例如：

- 新建文件
- 新建目录
- 修改代码
- 修改普通 UI
- 创建配置

不得因为“环境已经发生变化”而重新触发完整环境审查。

只有出现实质变化时，才进行相关的 Delta Check，例如：

- Node / Python 等运行时版本变化
- 新依赖安装
- 数据库 Schema 变化
- Docker 配置变化
- Git 基线变化
- 关键环境配置变化
- 实际环境与提示词发生冲突
- 核心测试异常且怀疑与环境相关

---

## 8. Anti-Loop Rule

禁止：

环境检查
→ 自动修改
→ 因修改再次完整检查
→ 再修改
→ 无限循环

对于同一根因：

默认最多允许：

一次自动修正
+
一次重新验证

仍然无法确认时：

返回 BLOCKED。

不得无限自动尝试。

---

## 9. Issue Severity

问题统一分级：

### BLOCKER

例如：

- 项目无法继续运行
- 数据损坏风险
- 严重安全问题
- 核心环境不可用

阻断后续执行。

### CORE

当前阶段核心目标无法成立。

阻断当前阶段。

### DEFERRED

不影响核心功能，可由后续技术人员处理。

记录后允许继续。

### COSMETIC

例如：

- 非关键 UI 微小误差
- 非关键动画细节
- 非关键格式问题
- 不影响功能的轻微体验问题

通常不阻断项目。

不得把以下问题作为普通技术债忽略：

- 明显安全漏洞
- 密钥泄漏
- 权限绕过
- 注入漏洞
- 任意文件访问
- 数据丢失风险
- 核心业务错误
- 明显核心功能 Bug

---

## 10. External Research

AI 在以下情况应优先检查外部已有方案：

- 新项目启动
- 新核心模块
- 技术架构选择
- 准备自行实现常见能力
- AI 对相关技术不确定
- 重大 Bug 长时间无法解决

优先参考：

- 官方文档
- GitHub
- 成熟开源项目
- 官方 SDK
- 公认稳定库

普通小修改不要求每次重新搜索。

外部参考应记录为：

ADOPT
ADAPT
REFERENCE
REJECT

不得看到开源项目后无审查直接复制。

---

## 11. Reference Reuse

已有可靠研究结果应优先复用。

只有出现以下情况才重新调查：

- 参考已过期
- 技术版本变化
- 进入新的技术领域
- 原方案失败
- 架构发生重大变化
- 需要最新事实

未来应通过 Reference Registry 管理高价值参考。

---

## 12. Skill Governance

Skill 的治理规则属于 Prompt Standard。

真正的 Skill 存放在独立中央目录：

D:\AI Building_Skills

Skill 不应全部复制进每一个项目。

Skill 使用模式：

TASK
→ Skill Registry Discovery
→ Skill Selection
→ Load Required Skill
→ Execute

禁止每次任务加载所有 Skill。

---

## 13. Skill Classification

Skill 分为：

GLOBAL

跨项目通用能力。

DOMAIN

某一技术领域可复用能力。

PROJECT

某一个项目专属能力。

ONE-OFF KNOWLEDGE

一次性知识，不直接创建 Skill。

---

## 14. Skill Promotion Rule

不得每遇到一个问题就建立 Skill。

建议生命周期：

Experience
→ Reference
→ Repeated Pattern
→ Skill Candidate
→ Formal Skill

正式 Skill 至少应满足：

- 可重复
- 较稳定
- 边界明确
- 具有实际复用价值

---

## 15. Standard and Skill Resolution

AI 在生成正式 Agent Prompt 前，应执行：

读取项目 Bootstrap
→ 获取当前 Prompt Standard
→ 查询 Standard Registry
→ 查询 Skill Registry
→ 选择相关 Skill
→ 查询 Reference
→ 必要时进行 Web / GitHub 调查
→ 形成方案
→ 生成 Execution Block Prompt

AI 不应无条件读取全部规范正文和全部 Skill。

采用 Registry First 原则。

---

## 16. Prompt Structure

正式施工提示词原则上包含：

### Layer 1 - Prompt Self Check

检查：

- Task / Block 标识
- 唯一目标
- 上游状态
- 执行范围
- 禁止范围
- 环境需求
- Skill 需求
- 测试要求
- 反馈格式
- 未知事项

发现关键未知条件时：

BLOCKED

不得伪造答案。

### Layer 2 - Owner Explanation

用 Owner 可以快速理解的语言说明：

- 做什么
- 为什么做
- 会影响什么
- 使用什么 Agent
- 使用什么 Skill
- 风险是什么
- 完成后如何验收

### Layer 3 - Dictionary

解释必要的技术术语。

### Layer 4 - Agent Execution Prompt

用于实际 Agent 执行。

必须明确：

- 目标
- 步骤
- 范围
- 禁止项
- Preflight
- 测试
- 报告格式

---

## 17. Agent Report

Execution Block 完成后必须返回：

- Block ID
- 目标
- 实际执行步骤
- 每一步结果
- 新增文件
- 修改文件
- 删除文件
- 测试结果
- 与提示词的偏差
- 已知问题
- BLOCKER / CORE / DEFERRED / COSMETIC
- 下一步建议

Agent 不得擅自启动未授权的下一重大区块。

---

## 18. Gate Model

Gate 分为三个层级：

### Step Gate

由 Agent 根据明确条件判断。

### Block Gate

由 AI 根据 Agent 反馈和证据判断。

### Owner Gate

只用于重要决策和重大风险。

这样既保持治理，又避免 Owner 成为普通施工过程的人工瓶颈。

---

## 19. Git Governance

Prompt Standard 使用：

Local Authoring Source
+
Git Published Source

当前本地 Authoring Source：

D:\AI Building_PromptStandard

Git 发布仓库：

https://github.com/ETlvein/AI-Building-PromptStandard

本地修改不等于正式发布。

只有：

Commit 成功
+
Push 成功

才认为进入 Published Source。

---

## 20. Publication States

规范和 Skill 至少区分：

LOCAL_DRAFT

仅存在于本地工作目录。

LOCAL_COMMITTED_NOT_PUBLISHED

已经 Git Commit，但尚未成功 Push。

PUBLISHED

已经成功 Push 到正式 Git 发布仓库。

只有 PUBLISHED 内容才允许其他项目把它视为正式可引用版本。

---

## 21. Git Evidence

涉及 Prompt Standard 或 Skill 修改时，Agent Report 应包含：

Repository
Branch
Commit SHA
Push Result
Registry Updated
Published Files

AI 可以通过 Git 发布仓库进行反向读取。

用于验证：

Agent 报告的内容
是否真实进入 Published Source。

---

## 22. Public Repository Safety

公开 Git 仓库不得包含：

- Password
- Token
- API Key
- Cookie
- SSH Private Key
- Certificate Private Key
- 数据库密码
- 患者数据
- 客户私有数据
- 未授权公开的商业秘密
- 其他敏感凭据

所有公开 Push 应进行 Public Repository Safety Check。

---

## 23. Bootstrap

不同项目不复制完整 Prompt Standard。

项目应通过轻量 Bootstrap 引用中央规范。

Bootstrap 至少应能够说明：

- Project ID
- Prompt Standard Repository
- Prompt Standard Version / Ref
- Standard Registry
- Skill Repository
- Skill Version / Policy
- Skill Registry
- Project-specific Standard

---

## 24. Version Stability

Prompt Standard 默认：

锁定明确版本。

不得让正在施工的稳定项目因为中央 main 更新而自动改变治理规则。

Prompt Standard 的升级应采用：

Explicit Standard Upgrade

Skill 可以根据项目风险选择：

LOCKED
COMPATIBLE_LATEST
LATEST

高风险项目优先 LOCKED。

---

## 25. Core Principle

整个体系的核心不是：

AI 说“完成了”。

而是：

REQUIREMENT
→ AUTHORIZATION
→ EXECUTION
→ EVIDENCE
→ AUDIT
→ ACCEPTANCE

通过这种方式建立可追踪、可验证、可复用的 AI 工程治理体系。

---

## 26. Current Status

PROMPT_STANDARD_V1.0

Status:

DRAFT

尚未冻结。

后续经过：

- 仓库初始化
- Registry 建立
- 初始模板建立
- Git 发布
- Git 反向验证
- Owner 最终确认

之后，才可以切换为正式冻结版本。
