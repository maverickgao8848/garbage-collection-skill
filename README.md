# Garbage Collection — 仓库审计与清理 Skill

A Claude Code skill that audits your repository against its own conventions and cleans up structural drift.

一个 Claude Code skill，根据项目 CLAUDE.md 中定义的规范审计仓库，清理结构漂移。

---

## What It Does / 功能说明

Scans your entire repo and checks for:

扫描整个仓库，检查以下问题：

| Check / 检查项                     | EN                                                    | 中文说明                                             |
| ---------------------------------- | ----------------------------------------------------- | ---------------------------------------------------- |
| **Directory structure compliance** | Missing or unexpected directories vs. CLAUDE.md       | 目录结构合规 — 缺失或多余的目录                      |
| **File placement**                 | Files sitting in the wrong location                   | 文件归位 — 文件放在了错误的位置                      |
| **Dependency layer violations**    | Lower layers importing from higher layers             | 依赖层违规 — 低层反向引用高层                        |
| **Index & reference integrity**    | Duplicate indexes, broken references, build artifacts | 索引与引用完整性 — 重复索引、断裂引用、构建产物      |
| **Skill integrity**                | Empty skill dirs, build artifacts in skill folders    | Skill 完整性 — 空 skill 目录、构建残留               |
| **Convention compliance**          | Sprint contracts missing fields, malformed workflows  | 规范合规 — sprint contract 缺字段、workflow 格式错误 |

---

## How It Works / 工作流程

1. **Read the rules / 读取规则** — Parses CLAUDE.md to extract prescribed structure, dependency hierarchy, and naming conventions
2. **Scan the repo / 扫描仓库** — Walks the entire file tree and catalogs every file's location, purpose, and relationships
3. **Run audit checks / 执行审计检查** — Six structured checks, each finding ranked as CRITICAL / WARNING / INFO
4. **Generate report / 生成报告** — Produces a structured markdown report with exact proposed actions
5. **Confirm & execute / 确认并执行** — Waits for your approval before touching anything

---

## Usage / 使用方式

Trigger with any of / 触发词：

```
/garbage-collection
gc
clean up repo
audit CLAUDE.md
garbage collection
清理仓库
审计
```

---

## Safety Guarantees / 安全保障

- **Never deletes** user content without explicit approval — 未经明确批准不会删除任何用户内容
- **Never modifies** CLAUDE.md — only flags issues — 不修改 CLAUDE.md，只标记问题
- **Report first, act second** — the audit report is the deliverable; cleanup is optional — 先报告后操作，清理是可选的
- **Preserves git history** — uses `git mv` over plain `mv` — 优先使用 `git mv` 保留 git 历史

---

## Audit Report Example / 报告示例

```markdown
# Garbage Collection Audit Report

**Date**: 2026-05-11
**Repo**: /path/to/project

## Summary / 摘要

| Severity | Count |
| -------- | ----- |
| CRITICAL | 1     |
| WARNING  | 3     |
| INFO     | 2     |

## CRITICAL Issues / 严重问题

### C1: Missing prescribed directory / 缺少规定目录

- **Location**: `projects/creator-hub/tests/e2e/`
- **Rule violated**: Directory structure — e2e test directory
- **Proposed action**: `mkdir -p projects/creator-hub/tests/e2e`
```

---

## Install / 安装

Copy the `garbage-collection/` folder into your project's skill directory:

将 `garbage-collection/` 文件夹复制到项目的 skill 目录：

```
# Project-level / 项目级
.agents/skills/garbage-collection/SKILL.md

# Global / 全局
.claude/skills/garbage-collection/SKILL.md
```

---

## License

MIT
