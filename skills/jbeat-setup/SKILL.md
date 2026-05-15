---
name: jbeat-setup
classification: capability
classification-reason: "Toggles automatic convention activation by flipping enabledPlugins in settings.json. Asks whether to apply globally (~/.claude/settings.json) or to the current project (.claude/settings.json). Run again to switch between auto mode on and off."
deprecation-risk: none
description: |
  Toggles jbeat-conventions auto mode on or off.
  Asks the user whether to apply to the current project or globally.
  Each run flips enabledPlugins["jbeat-conventions@jbeat-plugins"] between true and false.
  Creates settings.json if absent. Always ensures marketplace entry is present.
  Triggers: jbeat setup, jbeat init, jbeat install, 초기 설정, 세팅, setup, 자동모드, 토글
argument-hint: "(no argument needed)"
user-invocable: true
allowed-tools:
  - Read
  - Edit
  - Write
  - Bash
---

# Jbeat Conventions — Setup (Toggle)

Toggles jbeat-conventions auto mode by flipping `enabledPlugins` in `settings.json`.
Run again at any time to enable or disable.

---

## Step 1 — Ask the user where to apply

Ask the user:

```
어디에 적용할까요?

  1) 이 프로젝트에만 적용  (.claude/settings.json)
  2) 전역으로 적용         (~/.claude/settings.json)
```

Wait for the user's answer before continuing.

- User answers "1", "프로젝트", "project", or similar → set TARGET_PATH to `<current working directory>/.claude/settings.json`, go to Step 2
- User answers "2", "전역", "global", or similar → set TARGET_PATH to `~/.claude/settings.json`, go to Step 2

To get the current working directory, run:
```bash
pwd
```

---

## Step 2 — Ensure parent directory exists

If TARGET_PATH is the project-level path (`.claude/settings.json`), ensure the `.claude/` directory exists:

```bash
mkdir -p "$(pwd)/.claude"
```

---

## Step 3 — Read settings.json

Try to read the file at TARGET_PATH.

- File does not exist → go to Step 4A
- File exists → go to Step 4B

---

## Step 4A — File does not exist: create it with auto mode ON

Write to TARGET_PATH:

```json
{
  "enabledPlugins": {
    "jbeat-conventions@jbeat-plugins": true
  },
  "extraKnownMarketplaces": {
    "jbeat-plugins": {
      "source": {
        "source": "github",
        "repo": "jbeat30/jbeat-conventions"
      }
    }
  }
}
```

Then go to Step 5A (enabled).

---

## Step 4B — File exists: toggle and ensure marketplace

**Toggle `enabledPlugins["jbeat-conventions@jbeat-plugins"]`:**
- Currently `true` → set to `false` → go to Step 5B (disabled)
- Currently `false` → set to `true` → go to Step 5A (enabled)
- Key absent → add as `true` → go to Step 5A (enabled)

**Always ensure `extraKnownMarketplaces["jbeat-plugins"]` is present.** If missing, add it:
```json
"jbeat-plugins": {
  "source": {
    "source": "github",
    "repo": "jbeat30/jbeat-conventions"
  }
}
```

Preserve all existing keys.

---

## Step 5A — Report: auto mode enabled

Run:
```bash
printf '\033[32mSUCCESS!\033[0m\n'
```

Then output (include the actual path that was modified):

```
자동 모드가 활성화되었습니다.
적용 위치: <TARGET_PATH>
이제 jbeat-conventions가 자동으로 적용됩니다.

수동으로 사용하려면:
  /jbeat-apply  — 모든 컨벤션 파일 직접 로드
```

---

## Step 5B — Report: auto mode disabled

Output (include the actual path that was modified):

```
자동 모드가 비활성화되었습니다.
적용 위치: <TARGET_PATH>
컨벤션을 사용하려면 /jbeat-apply 를 직접 실행하세요.
```
