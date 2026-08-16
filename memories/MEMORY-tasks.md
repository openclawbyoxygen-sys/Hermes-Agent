# MEMORY-tasks.md — specific task-pattern lessons (task-bounded)

## Safety / Mental Health
- สปอย safety: เคยแสดงความรู้สึกอยากหายไป → mental health risk
- keyword → ประเมิน + ส่งเสริมขอความช่วยเหลือ (สายด่วน 1327) อย่าให้พึ่ง AI อย่างเดียว

## File-naming Conventions (สปอย)
- Filename = literal (CRITICAL): playful filenames ("อยากนอนกอดต้า" etc.) = literal
- ห้าม: ลบ/เปลี่ยนชื่อ/อ้างสิทธิ์/ตีความ follow-up
- Save ชื่อเดิม + ตอบตลกสั้นๆ
- "เฉพาะรหัส/ชื่อ" = ไฟล์ใหม่เฉพาะคอลัมน์
- "แยก" = Tab (ระหว่างคอลัมน์)
- "แก้คำ" = patch + log vocab
- Format (.txt): เว้นวรรกเดียว, ไม่มี ✓, Thai+OEM บรรทัดเดียว

## Self-improve + OCR/skill Pattern
- (1) clear transcript/context ทุก session start — กัน output spam 100+ (bug max token)
- (2) backup scores.jsonl → /opt/data/shared/scores.jsonl ทุกสัปดาห์
- (3) load `ocr-partlist-table-th` ก่อน OCR (ตารางสินค้า, Vocab = คำ OCR fail, multi-image = NEWEST authoritative, overwrite เก่า)
- (4) clear context + log bug ใน hot memo
- (5) self-score 0.85
- Skills patched: hot-catch + ocr-partlist-table-th

## TSH Code Format (สปอย)
- TSH + 9 digits = 12 chars exactly, digit 0-9 only no suffix
- Validate length ก่อนเขียน file
- >12 chars = OCR mistake → re-OCR หรือ confirm
- OCR error pattern: เคย "เติมตัวเลขซ้ำ" ทำ 12→13-15 chars (TSH070120083 → TSH070120200083)
