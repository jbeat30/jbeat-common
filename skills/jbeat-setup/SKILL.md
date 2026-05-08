---
name: jbeat-setup
classification: capability
classification-reason: "One-time initial setup command for the jbeat-conventions plugin. Writes the required entries into the user's ~/.claude/settings.json."
deprecation-risk: none
description: |
  Run once after installing jbeat-conventions to configure Claude Code automatically.
  Checks ~/.claude/settings.json for required entries and adds any that are missing.
  Reports SUCCESS (newly configured) or ALREADY SET (no changes needed).
  Triggers: jbeat setup, jbeat init, jbeat install, 초기 설정, 세팅, setup
argument-hint: "(no argument needed)"
user-invocable: true
allowed-tools:
  - Read
  - Edit
  - Write
  - Bash
---

# Jbeat Conventions — Initial Setup

Run this skill once after installing the jbeat-conventions plugin.
It will configure `~/.claude/settings.json` so that Claude Code loads the plugin automatically.

---

## Step 1 — Resolve the settings file path

Use Bash to resolve the actual path:

```
echo "$HOME/.claude/settings.json"
```

---

## Step 2 — Read the current settings

Read `~/.claude/settings.json`.

If the file does not exist, treat its contents as `{}` and proceed to Step 4.

---

## Step 3 — Check what is already configured

Check for both of the following entries:

**A. enabledPlugins entry**
```json
"enabledPlugins": {
  "jbeat-conventions@jbeat-plugins": true
}
```

**B. extraKnownMarketplaces entry**
```json
"extraKnownMarketplaces": {
  "jbeat-plugins": {
    "source": {
      "source": "github",
      "repo": "jbeat30/jbeat-conventions"
    }
  }
}
```

If both entries are already present → skip to Step 5 (report already configured).

---

## Step 4 — Add missing entries

For each missing entry, add it to the JSON object using Edit (if the file exists) or Write (if the file was absent).

Preserve all existing keys and values. Only add what is missing.

---

## Step 5 — Report result in Korean

### If newly configured (one or more entries were added):

```
✅ jbeat-conventions 설정 완료

추가된 항목:
- enabledPlugins에 "jbeat-conventions@jbeat-plugins" 추가
- extraKnownMarketplaces에 "jbeat-plugins" 등록

사용 가능한 명령어:
  /jbeat-conventions  — 현재 작업에 컨벤션 적용
  /jbeat-apply        — 모든 컨벤션 파일 수동 로드
```

### If already configured (no changes were needed):

```
✅ 이미 설정되어 있습니다

- enabledPlugins: jbeat-conventions@jbeat-plugins ✓
- extraKnownMarketplaces: jbeat-plugins ✓

별도 작업이 필요하지 않습니다.
```
