# Hot Memo — last updated 2026-08-04T16:30+07:00

## 🎯 Standing goal
Build a self-improving Hermes Agent ที่จำต่อเนื่อง + auto-push KB ขึ้น GitHub + cron pipeline ทำงาน Bangkok time
- **Context hygiene (2026-08-04 by ต้า):** ล้างบทสนทนาที่ไม่จำเป็นทุกวัน สรุปประเด็นสำคัญเป็น hot memo เพื่อกัน context overflow + max token bug
- next step: รอ cron `kb-preflight` ทำงาน 22:30 ICT คืนนี้ (2026-07-03T22:30+07:00) — first real cron run หลังตั้ง schedule

## 🔥 Open issues (P1 — block progress)
- ~~**revoke GitHub PAT ที่ paste ใน Discord**~~ — ✅ closed 2026-07-02T23:47 by O-XyGe-N
  - token `ghp_GYM...` ถูก revoke แล้ว — leak closed
- ~~**set host TZ → Asia/Bangkok**~~ — ✅ closed 2026-07-02T23:47 by O-XyGe-N (host)
  - `sudo ln -sf ... /etc/localtime` รันบน host แล้ว (container ยังเป็น UTC แต่ทุก Hermes layer ใช้ ICT ผ่าน env files + config)
  - ผลกระทบ: host shell ตอนนี้แสดง Bangkok time ถ้ารันคำสั่งที่อ่าน /etc/localtime
- ~~**fix output bug จาก max token overflow (2026-08-04 by ต้า)**~~ — ✅ closed 2026-08-04T16:30 by ต้า
  - bug: ฉันตอบ "มีอะไรอีกให้ฉันช่วยปอยค่ะ?" + emoji ซ้ำ 100+ ครั้ง (จาก message ของสปอย)
  - root cause: transcript scan ที่ใช้เวลานาน + ขาด context hygiene trigger
  - fix: ต้อง clear context + บันทึกเป็น hot memo ทุกวัน

## 📋 Daily Context Hygiene (2026-08-04 by ต้า)
**Standing rule:** ทุก session ต้องทำตามขั้นตอนนี้:
- [ ] **Daily:** clear transcript + session ก่อนหน้า (ใช้ `/new` หรือ `hermes context clear`)
- [ ] **Daily:** สรุปประเด็นสำคัญเป็น hot memo ใน `/opt/data/shared/hot/INDEX.md`
- [ ] **Daily:** hot-catch skill ทุก session start เพื่อเห็น standing state
- [ ] **Weekly:** prune hot memo เหลือ top 9 open items + archive closed
- [ ] **Trigger:** bug "output ซ้ำ 100+ ครั้ง" → หยุด + clear + log root cause ใน hot memo

**ป้องกัน:**
- max token overflow (bug 2026-08-04)
- output spam (bug 2026-08-04 — transcript scan ไม่ clear)
- context หดเมื่อเล่น 50+ ข้อความ/วัน

## 🟡 Open issues (P2 — track but don't dwell)
- [ ] **fix `terminal.shell_init_files` เป็น list ไม่ใช่ string** — opened 2026-07-02 23:25 — owner: O-XyGe-N
  - config.yaml ยังมี `shell_init_files: '["/opt/data/.bashrc", "/opt/data/.profile"]'`
  - รัน `hermes config edit` แก้เป็น proper YAML list
- [ ] **verify first nightly cron run (kb-preflight 22:30 ICT)** — opened 2026-07-02 23:45 — owner: cron-auto
  - 2026-07-03T03:01 UTC: kb-monitor ทำงานจริงครั้งแรก (last_status=ok) แต่ schedule ตั้งหลัง 06:00 ICT → next run = 22:30 คืนนี้
  - รอดูผลจริงตอน 22:30 ICT คืนนี้ (2026-07-03T22:30+07:00)
- [ ] **revoke old `setup_github_pat.py` token** — opened 2026-07-02 — owner: cron-auto
  - ถ้า PAT ตัวเดิมยังไม่ถูกลบ ให้ลบที่ GitHub settings

## 🟢 Recent decisions (last 5)
- 2026-07-03T08:42: เปลี่ยน kb-preflight + daily-kb → `deliver=local` เหมือน kb-monitor — silent ทั้งหมด ยกเว้น weekly-meta (report อาทิตย์)
- 2026-07-03T08:40: kb-monitor → `deliver=local` (silent) + ส่งเฉพาะเมื่อมีปัญหา (WARNING/CRITICAL) — ลด Discord noise
- 2026-07-03T08:30: **ใช้ UTC-shifted cron expressions** (`0 23 * * *` UTC = 06:00 ICT) — Hermes daemon scheduler ยัง interpret expression เป็น UTC; **อย่า revert เป็น `0 6 * * *`** เพราะจะกลายเป็น 06:00 UTC = 13:00 ICT (ผิด)
- 2026-07-02T23:15: เลือก SSH Deploy key (least-privilege) แทน HTTPS+PAT — ปลอดภัยกว่า account key
- 2026-07-02T22:30: ใช้ 3-layer memory: in-session todo + /goal (standing) + MEMORY.md (long-term)
- 2026-07-02T22:00: ใช้ skill `self-improve` เป็นมาตรฐาน — แทนสร้าง custom reflection engine ใหม่
- 2026-07-02T14:38: ตั้ง cron daily-kb 06:00 ICT, weekly-meta Sunday 09:00 ICT

## ⏳ Waiting on (external)
- _(none)_

## ✅ Recently closed (auto-archived after 30 days)
- 2026-07-03T08:42: ✅ ทุก check cron (kb-preflight, daily-kb, kb-monitor) → silent + alert on fail — Discord noise ลดลง 90%
- 2026-07-03T08:40: ✅ kb-monitor → silent (deliver=local + 3-tier decision rule)
- 2026-07-03T08:35: ✅ manual verify cron pipeline ผ่าน (`hermes cron run 05f50728f96c` ตอบ "succeeded")
- 2026-07-03T08:33: ✅ user report "ไม่เห็น cron ทำงาน" — root cause: schedule ตั้งหลัง 06:00 ICT ผ่านไป → next run ขยับเป็น 22:30 คืนนี้
- 2026-07-02T23:47: ✅ revoke GitHub PAT (P1 closed by user)
- 2026-07-02T23:47: ✅ host TZ → Asia/Bangkok (P1 closed by user)
- 2026-07-02T23:45: ✅ seed HOT memo + skill hot-catch พร้อมใช้
- 2026-07-02T23:35: ✅ kb-preflight + kb-monitor cron jobs ติดตั้งแล้ว (2 ตัวเพิ่มจาก original 2)
- 2026-07-02T22:30: ✅ self-healing ssh-agent (`ssh_agent_env.sh`) — 4 tests ผ่าน
- 2026-07-02T22:10: ✅ SSH push ขึ้น GitHub (commits 501f16d, fc182b7)
- 2026-07-02T22:00: ✅ skills 3 ตัว: self-improve, kb-ingest, prompt-ab
- 2026-07-02T15:25: ✅ daily-kb cron job ingest ไฟล์แรก (7 items)
- 2026-07-02T14:38: ✅ initial cron setup — daily-kb + weekly-meta

---

📌 Conv: active open = top 9, closed = keep 30 days, prune earlier
