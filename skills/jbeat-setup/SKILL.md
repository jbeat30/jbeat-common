---
name: jbeat-setup
classification: capability
classification-reason: "Toggles automatic convention activation by flipping enabledPlugins in ~/.claude/settings.json. Run again to switch between auto mode on and off."
deprecation-risk: none
description: |
  Toggles jbeat-conventions auto mode on or off.
  Each run flips enabledPlugins["jbeat-conventions@jbeat-plugins"] between true and false.
  Creates ~/.claude/settings.json if absent. Always ensures marketplace entry is present.
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

Toggles jbeat-conventions auto mode by flipping `enabledPlugins` in `~/.claude/settings.json`.
Run again at any time to enable or disable.

---

## Step 1 — Resolve path

```bash
echo "$HOME/.claude/settings.json"
```

---

## Step 2 — Read settings.json

Try to read `~/.claude/settings.json`.

- File does not exist → go to Step 3A
- File exists → go to Step 3B

---

## Step 3A — File does not exist: create it with auto mode ON

Write `~/.claude/settings.json`:

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

Then go to Step 4A (enabled).

---

## Step 3B — File exists: toggle and ensure marketplace

**Toggle `enabledPlugins["jbeat-conventions@jbeat-plugins"]`:**
- Currently `true` → set to `false` → go to Step 4B (disabled)
- Currently `false` → set to `true` → go to Step 4A (enabled)
- Key absent → add as `true` → go to Step 4A (enabled)

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

## Step 4A — Report: auto mode enabled

Run:
```bash
printf '\033[32mSUCCESS!\033[0m\n'
```

Then output:

```
자동 모드가 활성화되었습니다.
이제 jbeat-conventions가 자동으로 적용됩니다.

수동으로 사용하려면:
  /jbeat-apply  — 모든 컨벤션 파일 직접 로드
```

---

## Step 4B — Report: auto mode disabled

Output:

```
자동 모드가 비활성화되었습니다.
컨벤션을 사용하려면 /jbeat-apply 를 직접 실행하세요.
```
