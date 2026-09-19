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
4. 读取项目专属规则
5. 查询 Skill Registry
6. 只加载当前任务真正需要的 Skill
7. 必要时查询 Reference
8. 必要时进行 Web / GitHub / 官方文档研究
9. 完成分析后再生成 Execution Block Prompt

---

## Important Rules

不得默认使用中央仓库 main 的最新规则覆盖本项目锁定版本。

Prompt Standard 升级必须显式执行：

Explicit Standard Upgrade

不得因为存在 Skill Registry 而一次加载所有 Skill。
