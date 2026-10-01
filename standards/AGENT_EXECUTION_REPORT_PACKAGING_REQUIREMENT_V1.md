# AGENT_EXECUTION_REPORT_PACKAGING_REQUIREMENT_V1

Status: PUBLISHED

Version: 1.0

## Purpose

Define the mandatory packaging format for formal Agent execution feedback.

The objective is to prevent fragmented evidence delivery and establish a single auditable execution report package.

## Core Rule

All formal Agent Execution Feedback MUST be delivered as one ZIP package.

Accepted:

```
ONE EXECUTION REPORT ZIP PACKAGE
```

Rejected:

- scattered markdown/json/log files without package;
- chat-only completion claims;
- missing evidence linkage.

## ZIP Structure

Required structure:

```
/REPORT
    FINAL_EXECUTION_REPORT.md

/EVIDENCE
    evidence files

/CONTROL
    CONTROL_STATE_SNAPSHOT.json
    GATE_STATUS_SNAPSHOT.json

/HASH
    SHA256SUMS.txt

/LOG
    execution_log.txt

/MANIFEST
    PACKAGE_MANIFEST.json
```

## Required Report Content

FINAL_EXECUTION_REPORT.md MUST contain:

- BLOCK_ID
- PROJECT_ID
- TASK_ID
- execution environment
- execution result
- modified files
- unmodified files
- test results
- validation results
- final status

Claims such as "completed" or "passed" require linked evidence.

## Integrity Requirements

After ZIP creation, Agent MUST:

1. extract-test the package;
2. verify file completeness;
3. recalculate SHA256;
4. verify manifest consistency.

Only after successful verification:

```
PACKAGE_STATUS = VALID
```

## Final Chat Feedback Format

Agent final response SHOULD only contain:

```
EXECUTION_REPORT_PACKAGE_CREATED

ZIP:
<path>

PACKAGE_STATUS:
PASS / FAIL

SHA256:
<zip hash>

CONTROL_REVISION:
before -> after

FINAL_STATUS:
PASS / BLOCKED / FAILED
```

Large raw logs should remain inside ZIP.

## Audit Rule

AI Control Plane accepts formal execution evidence only from a verifiable ZIP package.

Missing package integrity data results in:

```
AUDIT_RESULT = BLOCKED
BLOCKER = INVALID_REPORT_PACKAGE
```

## Scope

Applies to:

- Execution Block
- Patch Task
- Gate Closure
- Owner Acceptance
- Audit Receipt
- Product Construction Task

Does not apply to:

- normal discussion;
- planning-only conversations;
- non-execution answers.
