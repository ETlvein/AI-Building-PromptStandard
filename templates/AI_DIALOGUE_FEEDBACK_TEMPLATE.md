# AI Dialogue Feedback Template

> **第 {CURRENT_STEP}/{TOTAL_STEPS} 步｜共 {TOTAL_PHASES} 个阶段｜当前：第 {CURRENT_PHASE}/{TOTAL_PHASES} 阶段「{PHASE_NAME}」｜本阶段第 {STEP_IN_PHASE}/{PHASE_TOTAL_STEPS} 步｜当前任务：{TASK_NAME}**

## 当前结论

用 3–8 行说明：

- 当前状态；
- 已完成什么；
- 当前唯一目标；
- 暂时不能做什么；
- 下一 Gate。

## 推荐思维强度：**{极低 / 低 / 中 / 高 / 极高 / 最大}**

**原因：**

根据复杂度、不确定性、跨系统范围、错误代价、可逆性、风险和证据要求说明推荐理由。

---

## 执行提示词

```text
这里放完整 Prompt。

Prompt Module 内只放真正需要复制给目标 AI / Agent / Codex 的内容。
不得混入对 Owner 的解释。
```

> 如果本轮没有 Prompt，则整个“执行提示词 + 提示词说明”区块省略。

## 提示词说明

| 项目 | 内容 |
|---|---|
| 目标 |  |
| 执行者 |  |
| 允许操作 |  |
| 禁止操作 |  |
| 核心动作 |  |
| 验收证据 |  |
| 阻断条件 |  |
| 下一 Gate |  |

### 这个提示词实际上会做什么

用自然语言简洁说明 Prompt 的真实执行逻辑。

---

# 详细说明

## 1. 最重要事项

……

## 2. 第二重要事项

……

## 3. 后续事项

……

---

## 当前限制与 Gate

```text
STATUS = ...
WRITE_PERMISSION = ...
OWNER_DECISION_REQUIRED = ...
BLOCKER = ...
NEXT_GATE = ...
```

---

## 下一步

**现在只做：{NEXT_ACTION}。**

---

## Delivery Rule

PROMPT_PRESENTATION = INLINE_WEB_PROMPT_MODULE

PROMPT_FILE_OUTPUT = EXPLICIT_USER_REQUEST_ONLY

除非用户明确要求真实文件、附件或下载交付物，否则不生成 Prompt 文件。
