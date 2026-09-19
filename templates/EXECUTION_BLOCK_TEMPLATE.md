# Execution Block Template

## Identity

PROJECT_ID:
BLOCK_ID:
BLOCK_NAME:

PROMPT_STANDARD_REF:

EXECUTION_AGENT:

REASONING_EFFORT:

---

## 1. Prompt Self Check

UNIQUE_OBJECTIVE:

UPSTREAM_STATE:

ALLOWED_SCOPE:

PROHIBITED_SCOPE:

ENVIRONMENT_REQUIREMENTS:

REQUIRED_SKILLS:

REFERENCE_REQUIREMENTS:

TEST_REQUIREMENTS:

UNKNOWN_ITEMS:

SELF_CHECK_STATUS:
PASS / BLOCKED

---

## 2. Owner Explanation

### 本区块做什么

### 为什么现在做

### 会修改什么

### 明确不做什么

### 需要什么 Agent

### 使用什么 Skill

### 主要风险

### 完成后 Owner 能看到什么

---

## 3. Relevant Preflight

只检查本 Execution Block 实际需要的环境。

禁止无意义进行全环境扫描。

检查结果：

PREFLIGHT_STATUS:
PASS / BLOCKED

---

## 4. Execution Steps

### STEP 01

ACTION:

EXPECTED_RESULT:

VALIDATION:

### STEP 02

ACTION:

EXPECTED_RESULT:

VALIDATION:

### STEP 03

ACTION:

EXPECTED_RESULT:

VALIDATION:

根据实际任务增加或减少步骤。

每一个实际步骤都必须反馈：

STEP:
ACTION:
STATUS:
RESULT:

---

## 5. Delta Check Rule

普通预期修改不得触发完整环境重审。

只有出现实质性环境变化或执行冲突时，才进行相关 Delta Check。

同一根因默认最多：

一次自动修正
+
一次重新验证

仍失败则：

BLOCKED

---

## 6. Testing

必须明确：

AUTOMATED_TEST:

BUILD_TEST:

REGRESSION_TEST:

MANUAL_TEST:

NOT_RUN_TESTS:

---

## 7. Issue Classification

发现问题时分类：

BLOCKER
CORE
DEFERRED
COSMETIC

BLOCKER 和 CORE 不得被隐藏为普通技术债。

---

## 8. Scope Control

Agent 不得：

- 擅自扩大需求
- 修改未授权核心架构
- 删除重要数据
- 创建未经授权的新重大功能
- 自行改变 Owner 已批准规则
- 自动进入未授权重大 Execution Block

---

## 9. Required Final Report

完成后必须按照：

AGENT_REPORT_TEMPLATE.md

返回执行报告。

最终状态只能根据实际情况填写：

PASS
PARTIAL
BLOCKED
FAILED

不得仅回复：

“完成”
“已修复”
“测试通过”
