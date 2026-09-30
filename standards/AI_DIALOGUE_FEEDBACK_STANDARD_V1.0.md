# AI Dialogue Feedback Standard V1.0

Standard ID: AI_DIALOGUE_FEEDBACK_STANDARD_V1.0

Status: FROZEN

Owner Approval: APPROVED

Freeze Date: 2026-09-30

Governed By: PROMPT_STANDARD_V1.0

## 1. Purpose

本规范统一规定跨项目网页 AI 对话反馈的默认呈现方式。

它负责回答：

- AI 如何组织网页反馈；
- AI 如何显示当前步骤与阶段；
- AI 如何推荐任务思维强度；
- Prompt 如何在网页中呈现；
- Prompt 后如何解释其用途；
- 什么时候可以生成真实 Prompt 文件；
- 详细说明、风险与下一步如何排列。

本规范不替代 PROMPT_STANDARD_V1.0。

PROMPT_STANDARD_V1.0 继续负责 Prompt 与 Agent 的核心治理；本规范负责 Owner 在网页对话中看到的反馈层。

---

## 2. Core Principle

网页 AI 对话反馈默认采用：

TOTAL
→ DETAIL

即：

先总后分。

Owner 应优先在页面顶部看到：

1. 当前在哪里；
2. 当前结论是什么；
3. 当前推荐的思维强度；
4. 如果存在 Prompt，直接可复制的 Prompt；
5. Prompt 实际会做什么；
6. 后续详细说明；
7. 风险 / Gate；
8. 唯一下一步。

不得把最重要结论埋在长篇正文末尾。

---

## 3. Mandatory Header

正式项目型网页反馈原则上以步骤抬头开始。

推荐格式：

第 {CURRENT_STEP}/{TOTAL_STEPS} 步
｜共 {TOTAL_PHASES} 个阶段
｜当前：第 {CURRENT_PHASE}/{TOTAL_PHASES} 阶段「{PHASE_NAME}」
｜本阶段第 {STEP_IN_PHASE}/{PHASE_TOTAL_STEPS} 步
｜当前任务：{STEP_NAME}

例如：

第 9/15 步｜共 4 个阶段｜当前：第 2/4 阶段「核心 Demo 软件构筑」｜本阶段第 5/6 步｜当前任务：V2 Fork / Rework Design Gate

### Unknown Total Rule

如果总步骤、总阶段或本阶段总步骤尚未锁定，不得伪造精确数字。

允许：

- 第 3/预计 8 步；
- 当前第 3 步｜总步数待 Architecture Review 后锁定；
- 本阶段步骤总数：UNKNOWN。

准确性优先于形式完整。

---

## 4. Current Conclusion

抬头后优先给出：

## 当前结论

通常控制在 3–8 行。

至少回答：

- 当前状态；
- 已完成什么；
- 本轮真正要做什么；
- 当前明确不能做什么；
- 下一 Gate 是什么。

此部分是 Total 层，不展开所有技术细节。

---

## 5. Reasoning Intensity Recommendation

当前结论之后给出：

## 推荐思维强度：{LEVEL}

允许等级固定为：

- 极低
- 低
- 中
- 高
- 极高
- 最大

这六级用于表达任务所需分析强度，不代表公开模型私有推理过程，也不要求展示隐藏 Chain of Thought。

### Evaluation Dimensions

推荐等级应综合：

- 任务复杂度；
- 不确定性；
- 跨文件 / 跨系统范围；
- 错误代价；
- 可逆性；
- 安全与数据风险；
- 证据要求；
- 架构影响。

### Level Guidance

极低：
格式化、状态确认、极简单转换、单值核对。

低：
单步骤、小范围、规则明确、低风险修改。

中：
常规多条件任务、普通开发、一般 Debug、多文件但边界清晰。

高：
复杂工程判断、Agent Prompt、跨文件修改、项目规划、技术路线、较复杂 Debug。

极高：
架构设计、复杂冲突、跨系统依赖、治理设计、重大根因分析。

最大：
高复杂度且高风险、高不可逆性或高证据要求，例如 Breaking Change、重大数据库迁移、破坏性 Git 操作、安全事件或正式冻结审计。

最大不等于默认最好。

简单任务不得为了形式而无意义推荐最大强度。

---

## 6. Prompt Presentation Policy

当网页反馈中需要交付 Prompt 时，默认使用：

INLINE_WEB_PROMPT_MODULE

而不是：

FILE_BY_DEFAULT

### Prompt Module

Prompt 必须放在独立模块中。

默认实现方式：

- 独立 fenced code block；
- 或客户端支持的原生独立可复制文本 / code / writing block。

目标体验：

- Prompt 与解释分离；
- 用户可以单独滚动长 Prompt；
- 客户端支持时提供一键复制；
- 一次复制即可获得完整 Prompt。

Prompt Module 内只放真正需要复制给目标 AI / Agent / Codex 的 Prompt 正文。

禁止混入：

- “下面请复制”；
- “我的建议是”；
- 对 Owner 的解释；
- Prompt 之外的审计说明；
- 与执行无关的聊天文字。

如果一次存在多个独立 Prompt，应使用多个独立 Prompt Module，不得把不同执行目标混成一个模块。

---

## 7. Default No-File Rule

Prompt 默认不得自动生成：

- .md；
- .txt；
- Word；
- PDF；
- ZIP；
- 附件；
- 下载文件；
- 其他真实 Prompt 文件。

默认交付方式是：

网页内 Prompt Module。

只有用户 / PROJECT OWNER 明确要求以下任一种时，才允许生成真实文件：

- “生成文件”；
- “给我附件”；
- “给我下载链接”；
- “保存成 .md / .txt / 其他格式”；
- 其他等价的明确文件交付要求。

不得因为 AI 自己认为“文件更正式”而自动生成文件。

如果某个外部工具链确实强制要求真实文件，AI 应先说明原因并取得授权，而不是静默改变交付方式。

---

## 8. Prompt Explanation

每个 Prompt Module 后必须提供：

## 提示词说明

推荐字段：

| 项目 | 内容 |
|---|---|
| 目标 | Prompt 最终解决什么 |
| 执行者 | ChatGPT / Codex / VS Code Agent / 其他 Agent |
| 允许操作 | Agent 可以做什么 |
| 禁止操作 | Agent 不能做什么 |
| 核心动作 | Prompt 主要执行逻辑 |
| 验收证据 | 最终必须返回什么 |
| 阻断条件 | 什么情况下必须停止 |
| 下一 Gate | 成功后进入哪里 |

随后可增加：

### 这个提示词实际上会做什么

用 Owner 可以快速理解的自然语言解释其实际作用。

不得要求 Owner 阅读完整 Prompt 后才能理解 Prompt 的目的。

---

## 9. Detailed Explanation

详细正文属于 Detail 层。

默认按照重要性降序：

MOST IMPORTANT
→ HIGH IMPACT
→ CURRENT REQUIRED
→ LATER
→ SUPPLEMENTARY

不得按照 AI 的思考顺序机械输出。

项目型反馈优先排列：

1. 为什么当前动作最重要；
2. 当前关键事实；
3. 影响范围；
4. 技术或业务说明；
5. 次要问题；
6. 后续事项；
7. 补充信息。

---

## 10. Risk and Gate Section

存在施工边界、风险、权限或治理 Gate 时，应单独给出：

## 当前限制与 Gate

可以使用紧凑状态块，例如：

STATUS = ...
WRITE_PERMISSION = ...
OWNER_DECISION_REQUIRED = ...
BLOCKER = ...
NEXT_GATE = ...

禁止把重大限制埋在普通正文中。

---

## 11. Unique Next Step

正式项目型反馈结尾默认给出：

## 下一步

在不存在 Owner 必须选择的真实分支时，只给一个明确的下一动作。

例如：

现在只执行：V2 Baseline Read-Only Audit。

不得无必要同时给出大量平行选择：

- 可以做 A；
- 也可以做 B；
- 还可以做 C；
- 你想选哪个？

只有出现真实决策分支、风险选择或 Owner Gate 时，才列出选项并等待 Owner 决策。

---

## 12. Canonical Web Feedback Order

默认顺序：

1. 步骤抬头
2. 当前结论
3. 推荐思维强度
4. Prompt Module（仅在需要 Prompt 时）
5. 提示词说明
6. 详细说明
7. 当前限制与 Gate（需要时）
8. 下一步

如果当前回答完全不涉及 Prompt，则跳过第 4–5 项，不得为了满足模板强行生成 Prompt。

---

## 13. Compactness Rule

规范的目标是提高可读性，不是让每次回复无限增长。

简单问题允许缩短。

复杂项目、Agent 施工、治理、架构或审计任务应使用完整结构。

不得为了“格式完整”重复相同信息。

---

## 14. Compatibility

本规范与以下基线兼容：

PROMPT_STANDARD_V1.0 / v1.0.0

冲突处理：

- Prompt 核心执行治理由 PROMPT_STANDARD_V1.0 负责；
- 网页反馈展示与 Prompt 交付形式由 AI_DIALOGUE_FEEDBACK_STANDARD_V1.0 负责；
- 项目专属规则可以进一步收紧，但不得静默放宽 Owner 已明确要求的 no-file 默认规则。

---

## 15. Owner Requirement Summary

Owner 已明确要求：

- 网页 AI 对话反馈采用总分结构；
- 抬头显示当前步骤、总步骤、阶段与阶段内步骤；
- 增加六级思维强度推荐并说明原因；
- Prompt 不默认以文件交付；
- Prompt 默认以网页独立模块展示；
- Prompt 模块应便于滚动与一键复制；
- Prompt 后必须说明 Prompt 做了什么；
- 详细说明按重要性排列；
- 除非明确要求，否则不生成 Prompt 文件。

以上要求为本标准 V1.0 的冻结治理语义。
