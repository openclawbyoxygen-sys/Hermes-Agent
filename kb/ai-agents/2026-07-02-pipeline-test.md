# ai-agents — 2026-07-02 (pipeline test)

## Manual test entry from cron pipeline verify

- Proves SSH deploy key works in fresh shell.
- Proves persistent ssh-agent can be re-used.
- Proves the push step at the end of `daily-kb` will succeed.

**Why it matters:** Without this verification, the cron job might silently fail to push for weeks.

**Tags:** #test #pipeline #verification

**Source URL:** local://cron-pipeline-test
