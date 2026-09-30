# Project AI Bootstrap Template

## Project Identity

PROJECT_ID:

PROJECT_NAME:

PROJECT_ROOT:

---

## Prompt Standard

PROMPT_STANDARD_REPOSITORY:
https://github.com/ETlvein/AI-Building-PromptStandard

PROMPT_STANDARD_REF:

CURRENT_STANDARD_FILE:
CURRENT_STANDARD.yaml

STANDARD_REGISTRY:
registries/STANDARD_REGISTRY.yaml

STANDARD_VERSION_POLICY:
LOCKED

---

## AI Dialogue Feedback Standard

DIALOGUE_FEEDBACK_STANDARD_ID:
AI_DIALOGUE_FEEDBACK_STANDARD_V1.0

DIALOGUE_FEEDBACK_STANDARD_PATH:
standards/AI_DIALOGUE_FEEDBACK_STANDARD_V1.0.md

DIALOGUE_FEEDBACK_POLICY:
REQUIRED_FOR_WEB_AI_DIALOGUE

PROMPT_PRESENTATION:
INLINE_WEB_PROMPT_MODULE

PROMPT_FILE_OUTPUT:
EXPLICIT_USER_REQUEST_ONLY

---

## Skill System

SKILL_REPOSITORY:

SKILL_REF:

SKILL_REGISTRY:

SKILL_VERSION_POLICY:
LOCKED / COMPATIBLE_LATEST / LATEST

---

## Project-Specific Governance

PROJECT_STANDARD_PATH:

PROJECT_RULES_PATH:

---

## AI Startup Procedure

AI进入本项目后应：

1. 读取本 Bootstrap
2. 获取指定 Prompt Standard
3. 读取 Standard Registry
4. 读取 AI Dialogue Feedback Standard
5. 读取项目专属规则
6. 查询 Skill Registry
7. 只加载当前任务真正需要的 Skill
8. 必要时查询 Reference
9. 必要时进行 Web / GitHub / 官方文档研究
10. 完成分析后再生成 Execution Block Prompt
11. 网页对话反馈按 AI Dialogue Feedback Standard 输出

---

## Important Rules

不得默认使用中央仓库 main 的最新规则覆盖本项目锁定版本。

Prompt Standard 升级必须显式执行：

Explicit Standard Upgrade

不得因为存在 Skill Registry 而一次加载所有 Skill。

网页对话中的 Prompt 默认使用独立的 Inline Prompt Module 展示，不默认生成 .md、.txt、附件或下载文件。

只有 PROJECT OWNER / 用户明确要求真实文件、附件或可下载交付物时，才生成 Prompt 文件。
