# jbeat-conventions

Shared Jbeat engineering conventions packaged as a Claude plugin skill.

This repository provides a reusable skill that guides implementation, review, refactoring, debugging, and planning work with a consistent Jbeat convention set.

## What It Covers

- Scope control and minimal safe changes
- Preserving existing behavior and contracts
- Naming and comment conventions
- Regression-risk awareness
- Honest validation and reporting

## Structure

- `skills/jbeat-conventions/SKILL.md`: skill metadata and core workflow
- `skills/jbeat-conventions/references/core-rules.md`: naming, comments, abstraction, error-handling rules
- `skills/jbeat-conventions/references/quality-checklist.md`: pre-work and final quality checklist
- `skills/jbeat-conventions/references/reporting-format.md`: final reporting format
- `.claude-plugin/plugin.json`: plugin packaging metadata
- `.claude-plugin/marketplace.json`: local marketplace metadata

## Installation

```bash
# 1. 마켓플레이스 등록 (최초 1회)
claude plugins marketplace add jbeat30/jbeat-conventions

# 2. 플러그인 설치
claude plugins install jbeat-conventions@jbeat-plugins
```

## Usage

```bash
# 컨벤션 적용
/jbeat-conventions

# 모든 컨벤션 파일 수동 로드
/jbeat-apply
```

## Repository Rename Note

Internal project and skill naming has been updated to `jbeat-conventions`.
If you also want the GitHub repository name changed, update that separately in GitHub settings and then adjust any remaining remote URLs as needed.
