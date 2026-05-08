---
name: jbeat-apply
classification: capability
classification-reason: "Explicitly loads all Jbeat convention reference files into context. Use when manually activating all conventions for a session or task."
deprecation-risk: none
description: |
  Manually load and activate all Jbeat engineering conventions.
  Use when you want to explicitly ensure all convention rules are loaded before starting work.
  Reads all reference files: core rules, naming, comment style, language policy, quality checklist, and reporting format.
  Triggers: jbeat apply, apply conventions, load conventions, 컨벤션 적용, 규칙 적용
argument-hint: "(no argument needed)"
user-invocable: true
allowed-tools:
  - Read
  - Bash
  - Glob
---

# Jbeat Conventions — Manual Load

Explicitly load all Jbeat engineering convention files into the active context.

## Steps

1. Use Bash to find the plugin installation path:
   ```
   find ~/.claude -path "*/jbeat-apply/references" -type d 2>/dev/null | head -1
   ```
2. Read each reference file from the resolved path in this order:
   - `core-rules.md`
   - `naming-conventions.md`
   - `comment-conventions.md`
   - `language-conventions.md`
   - `quality-checklist.md`
   - `reporting-format.md`
3. After reading all files, report to the user in Korean.

## After Loading

Confirm to the user in Korean which convention sets are now active:

- 코어 규칙 (개발 철학, 변경 원칙, 에러 처리, 구조)
- 네이밍 컨벤션 (이름 규칙, 변수/상수 규칙)
- 주석 컨벤션 (주석 스타일, JSDoc vs 인라인)
- 언어 컨벤션 (한국어 기본 정책, 예외 상황)
- 품질 체크리스트 (사전 확인, 안정성 기준, 금지 행동)
- 보고 형식 (결과 보고서 형식, 검증 보고 규칙)

이제 이 세션의 모든 작업에 위 규칙이 적용됩니다.
