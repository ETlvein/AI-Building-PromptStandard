# Prompt Standard Changelog

## [ADFS-1.0.0] - 2026-09-30

Standard:

AI_DIALOGUE_FEEDBACK_STANDARD_V1.0

Status:

FROZEN

Owner Approval:

APPROVED

### Added

- Cross-project web AI dialogue feedback standard
- Mandatory total-to-detail response structure
- Step / phase navigation header
- Six-level reasoning-intensity recommendation: 极低 / 低 / 中 / 高 / 极高 / 最大
- Inline web Prompt Module as the default Prompt delivery format
- Prompt explanation immediately after each Prompt Module
- Importance-descending detailed explanation
- Explicit risk / Gate section when applicable
- Unique next-step rule
- Default prohibition on Prompt file generation unless explicitly requested by the user
- AI Dialogue Feedback template
- Bootstrap discovery of the companion feedback standard

### Compatibility

- PROMPT_STANDARD_V1.0 remains unchanged and FROZEN.
- This is a companion governance standard, not a rewrite of the frozen core standard.

## [1.0.0] - 2026-09-19

Current Standard:

PROMPT_STANDARD_V1.0

Status:

FROZEN

Owner Approval:

APPROVED

### Added

- Central Prompt Standard repository architecture
- Local Authoring Source and Git Published Source model
- CURRENT_STANDARD.yaml
- STANDARD_REGISTRY.yaml
- PROMPT_STANDARD_V1.0
- Execution Block model
- Agent INSPECT -> EXECUTE -> REPORT model
- Block-Level Preflight
- Delta Check
- Anti-Loop Rule
- BLOCKER / CORE / DEFERRED / COSMETIC classification
- External Research governance
- Reference reuse governance
- Skill governance
- Registry First principle
- Execution Block template
- Agent Report template
- Project AI Bootstrap template
- Git evidence requirements
- Public repository safety rules
- Cross-platform line-ending policy

### Release Validation

- Local repository verification: PASS
- Public repository safety check: PASS
- Initial Git commit: PASS
- Initial Git push: PASS
- Remote AI verification: PASS
- PROJECT OWNER final approval: PASS

### Versioning Rule

Major:
Breaking governance changes.

Minor:
Backward-compatible governance improvements.

Patch:
Documentation, wording, or non-behavioral corrections.
