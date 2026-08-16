# MEMORY-meta.md — general agent lessons (Hermes-wide)

## GitHub Identity
- User: openclawbyoxygen-sys. Repo: openclawbyoxygen-sys/Hermes-Agent. UID 288289671.

## Hermes Environment
- `~/.hermes/config.yaml` patch blocked → use `hermes config set` (list → `hermes config edit`)
- SSH deploy key: `/opt/data/.ssh/hermes-agent-deploy` (ed25519)
- Persistent agent: `/opt/data/.ssh/agent.sock`
- Env loader: `/opt/data/.hermes_tmp/ssh_agent_env.sh` self-heals TZ from `~/.bashrc`

## Cron Behavior Pattern
- Silent-by-default: NORMAL=log only / WARNING=≤150 tokens Discord / CRITICAL=full alert
- Apply to ALL cron jobs unless user opts out

## Memory Hygiene Rules
- Trigger prune at 1,500 chars (not 2,200)
- `wc -c` both files → cross-ref USER→MEMORY → merge short entries
- Verify post-merge < pre-merge to confirm no info loss
- Strip date stamps during merge
- "ไม่กระทบผลลัพธ์" = stop at 1 round of pruning
- Scope: USER.md = user facts, MEMORY.md = agent lessons — do not merge across files

## File Splitting Strategy
- MEMORY-meta.md (this file) = Hermes-wide lessons (any agent can read)
- MEMORY-tasks.md = specific task lessons (OCR, syntax patterns, etc.)
- Both untracked by Hermes char limit; read via RAG layer in self-improve skill
