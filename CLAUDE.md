# tandem-hq — Amanda's Task Manager

## What this is
Personal task manager deployed as a static site on GitHub Pages.
Live URL: https://amandaposthuma.github.io/tandem-hq/

## Stack
- Single file: `index.html` — all HTML, CSS, JS in one file
- No build step, no framework
- State stored in `localStorage` key: `tandem_hq_v4`
- Deployed via GitHub Pages (push to main = live)

## Source of truth — DECISION: tandem-hq only
**Notion is no longer used for task management.** Tasks live here exclusively.
- Amanda adds tasks by telling Claude, or directly in the app
- Claude updates `CLAUDE_SYNC` when asked for a sync pass
- The Inbox (`CLAUDE_PROPOSALS`) is where Claude proposes new tasks — Amanda accepts or dismisses

## Key code blocks in index.html
- `// CLAUDE_DATA_START` → `// CLAUDE_DATA_END` — Claude rewrites this block with the full task list
- `// CLAUDE_PROPOSALS_START` → `// CLAUDE_PROPOSALS_END` — Claude writes proposed tasks here for Inbox review
- `localStorage key: tandem_hq_v4` — all user state (done status, notes, subtasks, images, vboard)

## Task ID conventions
- `t1`–`t99` and `n1`–`n20` — CLAUDE_SYNC managed tasks
- `u` prefix (e.g. `uab3x9`) — user-created tasks in the app (never purge these)
- `p` prefix — proposed inbox items (not yet accepted)

## loadState() purge rule
After merging CLAUDE_SYNC, any task ID that is NOT `u`-prefixed AND NOT in current CLAUDE_SYNC is removed.
This prevents stale IDs from old sync versions accumulating (was causing 170-task count).

## Buckets
| ID | Color | Label |
|---|---|---|
| HKH | #8b5cf6 | HKH Paris |
| FGC | #ef4444 | FGC Advisors |
| Vital Hackers | #22c55e | Vital Hackers |
| Tandem | #f59e0b | Tandem |
| Anne & Antonio | #06b6d4 | Anne & Antonio |
| Strides | #10b981 | Strides |
| SHIF | #f97316 | SHIF |
| Personal | #ec4899 | Personal |

## HKH task structure (as of Jun 17, 2026)
- **OT Part 1 — Aitana & Laiz:** reporting workflow setup, data room, Lais files
- **OT Part 2 — Alice & Ana:** demo scheduling, PPT follow-ups, workflow instructions
- **OT Part 3 — Tatiana:** Qonto integration, billing flow mapping (both due Jun 30)
- **Proposal Generator:** skill building, formatting, image imports, invite-only
- **Profitability:** KPI reporting, profitability meeting prep
- **HKH Misc:** Stephanie (Tephy) design system + Claude account, Claude expert, Cowork monitoring

## FGC task structure (as of Jun 17, 2026)
- **Website:** designer drafts, About Us, team page (t27 due Jul 1), developer briefs
- **Cloud/Workspace:** Clio, M365, QuickBooks, Dropbox, integrations, eSignature
- **Social Media:** Claude skills for social, newsletters, Instagram, Ali video critique
- **Other:** meeting prep, client reporting scope, process mapping

## Subtasks
Stored in `S.taskData[taskId].subtasks = [{text, done}]`
Rendered in task detail panel. Progress shown on task cards ("1/3 subtasks").

## Status as of Jun 17, 2026
- 87 tasks (deduplicated from 170)
- All bucketing organized
- Subtask checkboxes: done
- Inbox feature: done
- Notion sync: abandoned — tandem-hq is sole source of truth

## Next session: start here
1. Answer 4 remaining consolidation questions:
   - t17 (KPI reporting) + t21 (Translate KPIs) — merge or keep separate?
   - t3 + t59 + t16 (all Stephanie/Tephy) — merge or keep as steps?
   - t45 + t46 (Strides Brazil research) — merge?
   - t29 + t31 (FGC infra scoping) — merge?
2. What to do with Notion task database (delete, archive, ignore)?
