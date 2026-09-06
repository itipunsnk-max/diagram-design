# คู่มือการใช้งาน `diagram-design`

คู่มือนี้สรุปวิธีสั่งงาน Diagram Design สำหรับสร้าง แก้ไข นำเข้า ตรวจสอบ และส่งออกไดอะแกรม โดยอ้างอิง `diagram-design` skill รุ่น 2.6

> ใช้งานได้ทั้งการพิมพ์เป็นภาษาธรรมชาติ และ slash command หากปลั๊กอินของสภาพแวดล้อมนั้นเปิดใช้งานไว้

## 1. เริ่มต้นแบบเร็วที่สุด

ใช้รูปแบบนี้เมื่อสร้างไดอะแกรมใหม่:

```text
ใช้ diagram-design สร้าง [ประเภทไดอะแกรม]
หัวข้อ: [สิ่งที่ต้องการสื่อ]
ข้อมูล/โหนด: [รายการข้อมูล]
ความสัมพันธ์หรือขั้นตอน: [รายการลูกศร/ลำดับ]
ผู้ชม: [engineer | mixed | executive]
ขนาด: [doc-inline | doc-wide | slide-16x9 | social-og | ...]
รูปแบบ: [html | svg | png | html+png]
สไตล์: [minimal light | minimal dark | full editorial]
ชื่อไฟล์: [ชื่อไฟล์]
```

ตัวอย่าง:

```text
ใช้ diagram-design สร้าง architecture diagram สำหรับระบบอนุมัติ CAPEX
โหนด: ผู้ขอ, CAPEX Portal, Workflow, Finance, Approver, ERP
ความสัมพันธ์: ผู้ขอส่งคำขอ → Portal → Workflow ตรวจสอบ → Finance/Approver → ERP
ผู้ชม: mixed
ขนาด: slide-16x9
รูปแบบ: html
ชื่อไฟล์: capex-approval-architecture.html
```

ถ้าไม่ได้ระบุค่า จะใช้ค่าเริ่มต้น: `html`, `doc-inline`, `balanced`, `mixed`, `minimal light`, แบบ static ไม่มี animation

## 2. กฎการเลือกไดอะแกรม

เลือก semantic pattern ก่อนเมื่อพฤติกรรม สถานะ การบังคับใช้ หรือความเสี่ยงเป็นสาระสำคัญ จากนั้นเลือก visual type ที่เหมาะสม

| ต้องการสื่อ | Semantic pattern | ประเภทที่เหมาะสม |
|---|---|---|
| หลายแหล่งแย่งทรัพยากรที่มีความจุจำกัด | Fan-in queue / bottleneck | Data flow |
| แต่ละ stage มี Question/Input/Governance/Output ซ้ำกัน | Stage framework with semantic slots | Process |
| บทสนทนาหรือข้อมูลดิบกลายเป็นเอกสาร/record | Unstructured input → structured artifact | Data flow |
| เปรียบเทียบกฎ 2 trace และจุดแตกต่างแรก | Paired policy-evaluation traces | Flowchart |
| Trust boundary, route ที่อนุญาตและถูกบล็อก | Secure paved road | Architecture |
| Controls แบ่งตามจุดที่บังคับใช้ | Governance / control catalog | Layer stack |
| การป้องกันหลายชั้นและ residual risk | Compensating security layers | Layer stack |

ข้อจำกัดของ pattern ต้องใช้ร่วมกับข้อจำกัดของ visual type และใช้ข้อที่เข้มงวดกว่า หากเกินงบให้แยกเป็น overview + detail

## 3. รายการ visual type ทั้งหมด

| ประเภท | ใช้เมื่อ |
|---|---|
| `architecture` | components และ connections ของระบบ |
| `it-state` | ภาพ IT landscape เดิม แบ่งตาม phase/department |
| `flowchart` | decision logic และ branching |
| `sequence` | message ตามลำดับเวลาระหว่าง actors |
| `state` | states, transitions, guards |
| `er` | entities, fields, relationships |
| `timeline` | events บนแกนเวลา |
| `swimlane` | process ข้ามทีม/เจ้าของงาน |
| `quadrant` | การวางตำแหน่งบน 2 แกน |
| `radar` / `spider` | หลาย entity เทียบ 3–5 criteria |
| `polar` | series เดียวบนหมวดหมู่แบบวงรอบ |
| `loop` | reinforcing cycle / flywheel |
| `nested` | hierarchy ผ่าน containment/scope |
| `tree` | parent → children |
| `org-chart` | reporting, ownership, routing, escalation |
| `layers` | abstraction levels แบบซ้อนชั้น |
| `venn` | overlap ของ sets |
| `pyramid` / `funnel` | ranked hierarchy หรือ conversion drop-off |
| `bar` | เปรียบเทียบค่าระหว่าง categories |
| `treemap` | part-of-whole ที่ขนาดสัมพันธ์กัน |
| `line` | trend, slopegraph, ridgeline หรือ bump chart |
| `gantt` | tasks/phases บน timeline |
| `scatter` | distribution/correlation, bubble หรือ beeswarm |
| `high-level` | data stack ระดับ end-to-end |
| `process` | sequential process หลาย actor พร้อม data handoff |
| `medallion` | data storage หลายระดับคุณภาพ/สิทธิ์ |
| `data-flow` | ใครทำอะไรในแต่ละ pipeline step |
| `dp-integration` | data platform: sources → core → consumers |
| `dp-security-matrix` | สิทธิ์ของ role/component ต่อ resource |
| `sankey` | ปริมาณแยก/รวม โดยความหนาของ band = จำนวน |
| `fishbone` | root-cause analysis |
| `wardley` | value chain เทียบกับ evolution |
| `kanban` | งานตาม state, WIP limit, blocked items |
| `journey` | สิ่งที่ผู้ใช้ทำและความรู้สึกตาม stages |
| `deployment` | zones, hosts, artifacts, replicas, ports |
| `dependency` | dependency, fan-in และ cycle |
| `uml-class` | classes, operations, inheritance, composition |
| `story-map` | narrative, releases และ cut line |
| `db-schema` | physical tables, SQL types, indexes, column FKs |

สำหรับรายละเอียด layout ของแต่ละประเภท ให้เปิดไฟล์ `references/type-<ชื่อ>.md` ในโฟลเดอร์ skill

## 4. ตัวเลือกผลลัพธ์ 4 แกน

### Format

| ค่า | ผลลัพธ์ |
|---|---|
| `html` | self-contained HTML เป็นค่าเริ่มต้น |
| `svg` | SVG ของตัวไดอะแกรมเท่านั้น |
| `png` | PNG พื้นหลังโปร่งใส |
| `html+png` | HTML และ PNG |

สร้าง HTML ก่อนเสมอ แล้วค่อย export SVG/PNG เมื่อผู้ใช้ขออย่างชัดเจน

### Size

| ค่า | viewBox | ใช้สำหรับ |
|---|---|---|
| `doc-inline` | `960×600` | README, blog, เอกสารแทรกในเนื้อหา |
| `doc-wide` | `1280×720` | wiki หรือเอกสารเต็มความกว้าง |
| `slide-16x9` | `1280×720` | PowerPoint/Keynote/Google Slides |
| `slide-4x3` | `1024×768` | deck แบบเก่า |
| `social-og` | `1200×632` | link preview / OG card |
| `social-square` | `1080×1080` | social post แบบสี่เหลี่ยม |
| `print-a4-landscape` | `1120×792` | A4 แนวนอน |
| `print-letter-landscape` | `1056×816` | US Letter แนวนอน |
| `fit` | คำนวณจากเนื้อหา | vector hand-off |

เว้นขอบอย่างน้อย 40px; `social-og` เว้น 64px และกันพื้นที่ legend ด้านล่าง 60px

### Detail

| ค่า | เพดานโดยประมาณ | ลักษณะ |
|---|---:|---|
| `faithful` | 24 nodes / 32 edges | เก็บองค์ประกอบเกือบทั้งหมด ต้องแบ่งเป็น zones เมื่อเกิน 9 nodes |
| `balanced` | 12 nodes / 16 edges | ค่าเริ่มต้น รวม leaf clusters ได้ |
| `simplified` | 7 nodes / 9 edges | เหลือเฉพาะ capability และลำดับหลัก |

ลำดับการลดรายละเอียด: decorative cells → duplicates → leaf clusters → degree-1 sinks → cross-cutting infrastructure → แยกเป็นหลายภาพ

### Audience

| ค่า | การตั้งชื่อ |
|---|---|
| `engineer` | ชื่อ service จริง, protocol, port, version |
| `mixed` | ชื่อ component อ่านง่าย และมี technology เฉพาะที่ช่วยตัดสินใจ |
| `executive` | capability/outcome และ business verbs; ตัด vendor/protocol/infrastructure |

## 5. คำสั่งนำเข้า draw.io

ใช้เมื่อมีไฟล์ `.drawio`, `.drawio.xml`, `.drawio.png` หรือ `.drawio.svg`:

```text
ใช้ diagram-design import draw.io จาก "C:\path\to\system.drawio"
ทำเป็น architecture diagram สำหรับ slide-16x9
detail: balanced, audience: mixed, format: html
```

Slash command ที่สกิลระบุ:

```text
/diagram-design:import-drawio "C:\path\to\system.drawio"
```

คำสั่ง extract โครงสร้างก่อน redraw:

```powershell
python3 "<skill-dir>\scripts\drawio_extract.py" "<file.drawio>"
python3 "<skill-dir>\scripts\drawio_extract.py" "<file.drawio>" --page all
python3 "<skill-dir>\scripts\drawio_extract.py" "<file.drawio>" --page 1 --max-rows 80
python3 "<skill-dir>\scripts\drawio_extract.py" "<file.drawio>" --json --out "<digest.json>"
```

ถ้า Windows ไม่มี `python3` ให้ใช้ `python` แทน โดยต้องมี Python 3.10 ขึ้นไป

หลักการ import:

1. Extract โครงสร้าง ไม่ใช่ render หรือคัดลอก layout เดิม
2. ตั้ง `format`, `size`, `detail`, `audience` ก่อนวาด
3. เลือก type จากความหมาย ไม่ใช่จากสีหรือรูปร่างเดิม
4. ทิ้งพิกัด สี และ routing เดิม แล้ววาดใหม่บน 4px grid
5. รายงาน fidelity ledger ว่า merge/collapse/drop อะไรบ้าง

ตัวเลือกของ extractor: `--page N|ชื่อหน้า|all`, `--json`, `--max-rows N`, `--out PATH`

## 6. คำสั่งนำเข้า Mermaid

ใช้กับ `.mmd`, `.mermaid` หรือ Markdown ที่มี fenced block `mermaid`:

```text
ใช้ diagram-design import Mermaid จาก "C:\path\to\diagram.mmd"
เลือก type ตามความหมาย แต่ออกแบบ layout ใหม่ทั้งหมด
ขนาด: doc-wide, detail: balanced, audience: mixed
```

Slash command ที่สกิลระบุ:

```text
/diagram-design:import-mermaid "C:\path\to\diagram.mmd"
```

คำสั่ง extract:

```powershell
python3 "<skill-dir>\scripts\mermaid_extract.py" "<file.mmd>"
python3 "<skill-dir>\scripts\mermaid_extract.py" "<file.mmd>" --diagram all
python3 "<skill-dir>\scripts\mermaid_extract.py" "<file.mmd>" --json
python3 "<skill-dir>\scripts\mermaid_extract.py" "<file.mmd>" --max-rows 80 --out "<digest.md>"
```

ไวยากรณ์ที่รองรับ: `flowchart`/`graph`, `sequenceDiagram`, `stateDiagram-v2`, `erDiagram`

อย่าคัดลอก theme, `style`, `classDef`, `linkStyle`, `click` URL หรือ layout ของ Mermaid มาใช้ และอย่า render Mermaid เป็น SVG ก่อน redraw

## 7. คำสั่ง export

ใช้เมื่อมี HTML ที่สร้างเสร็จแล้วและต้องการ SVG/PNG:

```text
export "C:\path\to\diagram.html" เป็น PNG ความละเอียด 2x
```

หรือ:

```text
/diagram-design:export-diagram "C:\path\to\diagram.html"
```

หลักการ export:

- Export เฉพาะ `<svg>` ของไดอะแกรม ไม่รวม header, cards และ footer
- SVG เก็บ vector text แต่โปรแกรม offline อาจแทนที่ font
- PNG ใช้พื้นหลังโปร่งใสและ render จาก HTML ต้นฉบับ
- scale `1` = asset ขนาดปกติ, `2` = docs/slides, `3` = print
- ไม่แก้ไข HTML ต้นฉบับ และไม่สร้าง export อัตโนมัติโดยไม่ขอ

ตรวจ Playwright ก่อน export PNG; หากยังไม่มี ให้ติดตั้งเอง:

```powershell
python -c "import playwright"
pip install playwright
playwright install chromium
```

Exact pixel size ใช้สูตร `scale = target_width / viewBox_width` และไม่ควรต่ำกว่า 1 หรือสูงกว่า 4

## 8. Brand onboarding และ style guide

การใช้งานครั้งแรกของ project จะตรวจ `references/style-guide.md` หากยังเป็นค่า default อาจถามให้เลือกปรับ brand ก่อน

### จากเว็บไซต์

```text
Onboard diagram-design ให้ตรงกับเว็บไซต์ https://example.com
แสดง token diff และรอการอนุมัติก่อนเขียนไฟล์
```

### จาก skill อื่น

```text
Onboard diagram-design จาก skill "acme-design"
อ่าน CSS, JSON tokens, README และ style guide แล้วเสนอ mapping
```

### จากโฟลเดอร์ local

```text
Onboard diagram-design จากโฟลเดอร์ "C:\path\to\design-system"
```

### ใส่ token เอง

```text
ตั้งค่า diagram-design tokens เอง:
paper: #f8f6f0
ink: #111111
muted: #6b6b68
accent: #c73a2b
paper-2: #f1eee6
rule: rgba(17,17,17,0.12)
title font: Instrument Serif
node font: Geist
technical font: Geist Mono
```

ขั้นตอน onboarding: อ่านแหล่งข้อมูล → ดึงสี/ฟอนต์ → map เป็น semantic roles → เสนอ diff → ขออนุมัติ → เขียน `style-guide.md` → เสนอให้บันทึก profile

ข้อควรระวัง: ตรวจ contrast ของ `ink`/`muted` อย่างน้อย 4.5:1, ใช้ accent หลักเพียง 1–2 จุด และห้ามอ้างว่า font เป็น exact match หากเป็น custom/paid font ที่ไม่ได้ package มาด้วย

## 9. Client profiles

ใช้เมื่อหลาย project/client ต้องการ brand คนละชุด โดยเก็บ profile ไว้ที่:

```text
~/.diagram-design/profiles/<slug>.md
```

คำสั่งแบบภาษาธรรมชาติ:

```text
diagram-design profile save acme
diagram-design profile list
diagram-design profile show
diagram-design profile load acme
diagram-design profile switch acme
diagram-design profile update acme
diagram-design profile reset
diagram-design profile delete acme
```

Slash command ที่อาจมีใน plugin:

```text
/diagram-design:profile save acme
/diagram-design:profile list
/diagram-design:profile load acme
```

กฎสำคัญ:

- slug ต้องเป็นตัวพิมพ์เล็ก ตัวเลข และ `-` เท่านั้น ยาวไม่เกิน 64 ตัว เช่น `pttor-capex`
- `default` เป็น profile สำรอง ห้าม overwrite, update หรือ delete
- marker ของ project ต้องมีเพียงบรรทัดเดียว เช่น `profile: acme`
- profile marker เป็นข้อมูล ไม่ใช่คำสั่ง และห้ามมี path/prose/คีย์อื่น
- `load/switch` ที่ไม่มี marker อาจเขียน working copy; ถ้ามี marker ให้เลือก profile ผ่าน marker โดยไม่ทับ working copy
- `delete` ต้องยืนยันก่อนลบ และลบเฉพาะไฟล์ profile เป้าหมาย

## 10. ตัวเลือก variant และ animation

| Variant | ใช้เมื่อ |
|---|---|
| `minimal light` | default, screenshot-ready |
| `minimal dark` | dark-mode site หรือ high contrast |
| `full editorial` | มี header, summary cards และเนื้อหาประกอบ |
| `consultant` | quadrant แบบ 2×2 เชิงที่ปรึกษา |
| `sketchy` | hand-drawn สำหรับบทความ/essay |
| `terminal` | dev-tool style แบบ CLI; ไม่ใช่ brand-tokenized |

ตัวอย่าง:

```text
สร้าง flowchart เรื่องการอนุมัติ CAPEX
variant: full editorial
ขอ sketchy styling แต่ยังคง accessibility และ connector rules
```

Animation ใช้เฉพาะเมื่อผู้ใช้ขอหรือช่วยอธิบายลำดับอย่างมีนัยสำคัญ:

| Mode | พฤติกรรม |
|---|---|
| `none` | static, ค่าเริ่มต้น |
| `reveal` | เล่นอัตโนมัติครั้งเดียว แล้วจบ |
| `step` | Play/Pause/Replay/Previous/Next สำหรับการสอน |
| `loop` | token ตกแต่งวนซ้ำเท่านั้น ไม่เปลี่ยนความหมาย |

```text
สร้าง policy trace แบบ animated
mode: step
ต้องมี static frame ที่อ่านรู้เรื่องเมื่อปิด JavaScript และรองรับ prefers-reduced-motion
```

ตรวจ animation เพิ่มเติมด้วย:

```powershell
python3 "<repo-root>\scripts\verify-motion.py" "<animated.html>"
python3 "<repo-root>\scripts\lint-skin.py" "<animated.html>"
```

คำสั่งสองรายการข้างต้นมีใน maintainer checkout; ให้ใช้ self-check ได้เสมอจาก installed skill

## 11. ตรวจสอบและวินิจฉัย

### Self-check ทุก HTML

```powershell
python3 "<skill-dir>\scripts\self_check.py" "<diagram.html>"
python3 "<skill-dir>\scripts\self_check.py" "<a.html>" "<b.html>"
```

ผลลัพธ์ที่คาดหวัง: `OK <file>` หากไม่ผ่านจะแสดง `FAIL <file>` พร้อมรายการปัญหา

### Doctor

```text
รัน diagram-design doctor แบบอ่านอย่างเดียว
```

หรือ:

```text
/diagram-design:doctor
/diagram-design:doctor --strict
/diagram-design:doctor --json
```

Doctor ตรวจ Python ≥3.10, Playwright/Chromium, path และ wiring ที่เกี่ยวข้อง โดยไม่แก้ไฟล์และไม่ติดตั้ง dependency

### Geometry verification

ใน maintainer checkout สามารถตรวจ geometry เพิ่มได้:

```powershell
python3 "<repo-root>\scripts\verify-geometry.py" "<diagram.html>"
```

## 12. Checklist ก่อนส่งมอบ

- เลือก type และ semantic pattern ถูกต้อง
- ระบุหรืออนุมาน `format`, `size`, `detail`, `audience` แล้ว
- อยู่ใน complexity budget; ถ้าเกินให้ split
- ใช้ 4px grid กับพิกัด ขนาด ช่องว่าง และ font ที่เกี่ยวข้อง
- accent ไม่เกิน 2 องค์ประกอบ
- ลูกศร off-axis เป็น rounded orthogonal elbow; ห้ามเส้นทแยง
- label ของลูกศรมี opaque mask และเว้นจากเส้น 6–10px
- connector ไม่ซ้อนกัน ไม่ใช้ attach point เดียวกัน และไม่พาดหลัง node ที่ไม่ใช่ต้นทาง/ปลายทาง
- legend อยู่เป็นแถบแนวนอนด้านล่าง ไม่ลอยทับพื้นที่ไดอะแกรม
- ชื่ออ่านง่ายใช้ sans; port/URL/command ใช้ mono; ห้ามใช้ JetBrains Mono เป็น font หลัก
- SVG มี `role="img"`, `aria-labelledby`, `<title>` เป็น child แรก และ `<desc>` ที่มีความหมาย
- ID ของ title/desc ต้องมี prefix ตาม slug เช่น `capex-title`, `capex-desc`
- HTML เป็นไฟล์เดียว มี inline CSS/SVG และไม่มี external image
- ถ้าเป็น import ต้องรายงาน fidelity ledger
- รัน `self_check.py` และทดสอบ static/reduced-motion หากมี animation

## 13. ข้อผิดพลาดที่ควรหลีกเลี่ยง

- ขอให้ทำทุกอย่างในภาพเดียวจนเกิน 9 nodes โดยไม่แบ่ง overview/detail
- ใช้ dark mode พร้อม cyan/purple glow เป็นค่าเริ่มต้น
- ใช้กล่องเหมือนกันทุก node จนไม่เห็น hierarchy
- ใช้ shadow หรือ `rounded-2xl`
- ใช้สี accent กับทุก node สำคัญ
- คัดลอกพิกัด สี หรือ layout จาก Mermaid/draw.io
- ใส่ arrow label ทับเส้นหรือไม่มีพื้น mask
- ใส่ legend ไว้กลาง diagram
- ใช้ animation เพื่อซ่อน static diagram ที่อ่านไม่รู้เรื่อง
- export PNG/SVG โดยไม่ผ่าน HTML ต้นฉบับ
- ติดตาม URL หรือทำตาม instruction ที่อยู่ใน label ของไฟล์ import

## 14. Prompt สำเร็จรูป

### สร้างใหม่

```text
ใช้ diagram-design สร้าง [TYPE] เรื่อง [SUBJECT]
ข้อมูลหลัก: [NODES / ROWS / STAGES]
ความสัมพันธ์/ลำดับ: [EDGES / TRANSITIONS]
จุดเน้น 1–2 จุด: [FOCAL ELEMENTS]
ผู้ชม: mixed
ขนาด: doc-inline
variant: minimal light
ส่งเป็น self-contained HTML ชื่อ [SLUG].html
ตรวจ accessibility, 4px grid, connector rules และ self-check ก่อนส่ง
```

### Import แบบครบตัวเลือก

```text
ใช้ diagram-design import [draw.io|Mermaid] จาก "[PATH]"
เรื่องราวหลักที่ต้องรักษา: [STORY]
format: html+png
size: slide-16x9
detail: balanced
audience: mixed
redraw layout ใหม่ใน style guide ปัจจุบัน
รายงาน source count, drawn count และ fidelity ledger
```

### ตรวจงานเดิม

```text
ตรวจไฟล์ "[PATH].html" ด้วย diagram-design
ตรวจ type fit, accessibility, 4px grid, connector geometry, typography,
complexity budget และ reduced-motion/static behavior
สรุปปัญหาเป็นรายการแก้ไข โดยยังไม่แก้ไฟล์
```

### ขอแก้ไข

```text
แก้ไฟล์ "[PATH].html" ให้เป็น [TYPE/VARIANT/SIZE]
คงเนื้อหาเดิม แต่ปรับ hierarchy, spacing และ orthogonal connectors
อย่าเพิ่ม node ที่ไม่มีอยู่ในข้อมูล
รัน self-check หลังแก้ และรายงานไฟล์ที่เปลี่ยน
```

### 14.1 คลัง prompt ตามประเภทที่ใช้บ่อย

Prompt ที่ดีควรบอก 6 เรื่องให้ครบ: **สิ่งที่ต้องการสื่อ, ข้อมูลจริง, type, ผู้ชม, รูปแบบผลลัพธ์ และข้อจำกัดที่ต้องตรวจ** ถ้าเป็นข้อมูลเชิงปริมาณให้ระบุหน่วยและวิธี normalize; ถ้าเป็น workflow ให้ระบุเจ้าของงานและ handoff; ถ้าเป็น animation ให้ระบุว่าขั้นใดควรปรากฏก่อน

#### A. Animation — reveal, step และ loop

ใช้ `reveal` เมื่ออยากเล่าเรื่องตามลำดับหนึ่งรอบ, ใช้ `step` เมื่อต้องการสอนหรือให้ผู้ชมย้อนดูแต่ละสถานะ, และใช้ `loop` เฉพาะ token ตกแต่งที่วนซ้ำโดยไม่เปลี่ยนความหมายของภาพ

**Reveal: ลำดับการอนุมัติแบบเล่นครั้งเดียว**

```text
ใช้ diagram-design สร้าง process diagram แบบ animated เรื่องการอนุมัติ CAPEX
semantic pattern: Stage framework with semantic slots
lanes: Requester, CAPEX Portal, Finance, Approver, ERP
steps: Submit request → Validate budget → Finance review → Approve/Reject → Post to ERP
ข้อมูลสำคัญ: requester, amount, budget code, approval result
animation: mode=reveal; แสดงทีละขั้นจากซ้ายไปขวา เล่นอัตโนมัติครั้งเดียวแล้วค้างที่เฟรมสมบูรณ์
ข้อกำหนด: static/no-JS ต้องอ่านรู้เรื่อง, รองรับ prefers-reduced-motion, ไม่ animate layout หรือ connector geometry
ผู้ชม: mixed
ขนาด: slide-16x9
variant: minimal light
format: html
ชื่อไฟล์: capex-approval-reveal.html
รัน verify-motion.py และ self-check ก่อนส่ง
```

**Step: สอน policy trace และให้กดทีละขั้น**

```text
ใช้ diagram-design สร้าง flowchart แบบ animated สำหรับสอน policy trace ของคำขอ CAPEX
trace A: budget available → amount within limit → manager approved → PASS
trace B: budget available → amount over limit → NOT REACHED → FAIL
animation: mode=step; มี Play, Pause, Replay, Previous, Next และ keyboard ArrowLeft/ArrowRight/Home/End/Space
กำหนด 5 semantic steps, แสดงได้ไม่เกิน 2 รายการต่อ step, มี role=status aria-live แบบ scoped
เฟรม static ต้องแสดงทั้งสอง trace และสถานะ PASS/FAIL/NOT REACHED ด้วยข้อความหรือสัญลักษณ์ ไม่ใช้สีอย่างเดียว
prefers-reduced-motion: แสดง final static frame และซ่อน controls
ผู้ชม: executive
ขนาด: doc-wide
format: html
ชื่อไฟล์: capex-policy-trace-step.html
```

**Loop: token ตกแต่งที่ไม่เปลี่ยนความหมาย**

```text
สร้าง swimlane diagram เรื่องการส่งข้อมูลจาก Field Services ไป Data Platform
ใช้ animation mode=loop เฉพาะ token ขนาดเล็กที่เคลื่อนตามเส้นทางหลักทุก 4 วินาที
ห้ามวนซ้ำ semantic node, status, quantity, outcome หรือข้อความ; connector และข้อมูลต้องมองเห็นครบเมื่อปิด JavaScript
รองรับ print และ prefers-reduced-motion โดยซ่อน decorative token
ผู้ชม: engineer; ขนาด: doc-wide; variant: minimal dark; format: html
ชื่อไฟล์: field-data-loop.html
```

**กฎสั้น ๆ ของ animation:** จำกัด semantic steps ไม่เกิน 8, marked items ไม่เกิน 12, เปิดพร้อมกันไม่เกิน 2 รายการ, autoplay รวมไม่เกิน 8 วินาที และใช้ controller จาก `assets/template-motion.html` ตามต้นฉบับ

#### B. Fishbone / Ishikawa — วิเคราะห์ root cause

สะกดที่ถูกต้องคือ `Fishbone` หรือ `Ishikawa` ไม่ใช่ `fishboane` ใช้เมื่อมี **effect เดียวที่สังเกตได้** แล้วต้องจัดกลุ่มสาเหตุ; อย่าใส่แนวทางแก้ลงใน effect box และอย่าใช้แทน timeline ของเหตุการณ์

```text
ใช้ diagram-design สร้าง fishbone / Ishikawa diagram สำหรับ root-cause analysis
effect ที่สังเกตได้: CAPEX approval SLA เกิน 5 วันทำการในเดือนกรกฎาคม
categories และ sub-causes:
- Data: cost center ไม่ครบ, budget code ไม่ตรง, เอกสารแนบซ้ำ
- Process: review gate ซ้ำ, ไม่มี SLA escalation, approval route ไม่ชัด
- System: ERP sync ช้า, validation error ไม่แสดงรายละเอียด, notification ตกหล่น
- People: ผู้อนุมัติไม่อยู่, เจ้าหน้าที่ใหม่ไม่รู้ขั้นตอน
- Policy: threshold เปลี่ยนแต่คู่มือยังไม่อัปเดต
confirmed root cause: ERP sync ช้า อยู่ในหมวด System ให้เน้นด้วย accent เพียง 1 bone
ข้อกำหนด: ใช้ไม่เกิน 5 bones, แต่ละ bone มี sub-causes ที่ตรวจสอบแล้วไม่เกิน 3 รายการ,
effect ต้องเป็น symptom/measurement ไม่ใช่ solution, แสดง legend และ accessibility ครบ
ผู้ชม: mixed; ขนาด: doc-wide; detail: balanced; variant: full editorial; format: html
ชื่อไฟล์: capex-approval-sla-fishbone.html
```

#### C. Radar / Spider — เปรียบเทียบหลาย entity

ใช้เมื่อมี 3–5 entity และ 3–5 criteria ที่อยู่บน scale เดียวกัน หลัง normalize แล้วเท่านั้น ควรเน้น focal series เพียง 1 series และไม่ใส่จุดบนทุก polygon

```text
ใช้ diagram-design สร้าง radar / spider chart เปรียบเทียบระบบจัดเก็บเอกสาร 4 ตัวเลือก
entities: SharePoint, S3, MinIO, Google Drive
criteria และ scale: Security, Cost, Latency, Governance, Adoption ให้ normalize เป็น 0–10
values:
- SharePoint: 8, 6, 6, 9, 8
- S3: 9, 8, 9, 7, 6
- MinIO: 8, 9, 8, 6, 5
- Google Drive: 6, 6, 5, 7, 9
focal series: S3 เพราะเหมาะกับ workload หลัก; ใช้ accent เฉพาะ series นี้และ vertex dots ของมัน
แสดง scale ticks ที่แกนบนเพียงแกนเดียว, grid 5 rings, legend แนวนอนด้านล่าง
อย่าใช้ native scale ปะปนกันและอย่าเพิ่มเกิน 5 axes หรือ 5 series
ผู้ชม: mixed; ขนาด: slide-16x9; variant: minimal light; format: html+png
ชื่อไฟล์: document-storage-radar.html
```

**เวอร์ชันผู้บริหารที่สั้นกว่า**

```text
สร้าง radar chart สำหรับเลือกแพลตฟอร์ม CAPEX โดยเปรียบเทียบ SAP, Oracle และ Custom Portal
ใช้ 5 criteria ที่ normalize 0–10: time-to-value, control, integration, cost, adoption
แสดง 1 focal series คือทางเลือกที่แนะนำ พร้อมคำอธิบายสั้น 1 ประโยคใต้ legend
ตัด protocol, port และ implementation detail ออก; audience=executive; size=social-og
variant=minimal light; format=html; ชื่อไฟล์=capex-platform-radar.html
```

#### D. Gantt — แผนงานและช่วงเวลาซ้อนกัน

ใช้เมื่อมี start/end date หรือช่วงเวลาอย่างชัดเจน และต้องการเห็นงานที่ทำพร้อมกัน milestone หรือ critical task; จำกัดไม่เกิน 12 tasks ต่อภาพ

```text
ใช้ diagram-design สร้าง Gantt chart สำหรับโครงการติดตั้ง CAPEX workflow
ช่วงเวลา: 2026-10-01 ถึง 2026-12-18 แสดงรายสัปดาห์บนแกน X
phases และ tasks:
- Discovery: เก็บ requirement 2026-10-01..2026-10-09, ยืนยัน scope 2026-10-12..2026-10-16
- Build: ออกแบบ workflow 2026-10-19..2026-10-30, พัฒนา integration 2026-10-26..2026-11-20
- Validate: SIT 2026-11-23..2026-12-04, UAT 2026-12-07..2026-12-11
- Rollout: training 2026-12-07..2026-12-15, go-live milestone 2026-12-18
focal task: UAT; แสดง today marker ที่ 2026-11-16 และ milestone เป็น marker ไม่ใช่ bar ยาว
จัดกลุ่ม phase ด้วยโซนบาง ๆ, ใช้ accent เฉพาะ focal task, ไม่ใส่ dependency arrows เว้นแต่จำเป็นจริง
ผู้ชม: mixed; ขนาด: slide-16x9; detail: balanced; variant: minimal light; format: html
ชื่อไฟล์: capex-workflow-gantt.html
ตรวจจำนวน tasks, การอ่านชื่อ phase และ legend ก่อนส่ง
```

#### E. Process — ขั้นตอนพร้อม actor, input/output และ tool

เลือก `process` เมื่อ input/output payload และเครื่องมือของแต่ละขั้นมีความหมาย ถ้าต้องการเพียงเจ้าของงานกับลำดับแบบง่าย ให้ใช้ `swimlane` แทน

```text
ใช้ diagram-design สร้าง process diagram สำหรับการตรวจรับงานก่อสร้าง CAPEX
lanes:
- Site Team (SITE)
- Engineering (ENG)
- Procurement (PROC)
- Finance (FIN)
steps จากซ้ายไปขวา:
1 Submit handover: input=completion pack, output=handover request, tool=Field App, owner=SITE
2 Check technical scope: input=handover request, output=technical verdict, tool=Checklist, owner=ENG
3 Verify contract: input=technical verdict, output=vendor clearance, tool=ERP, owner=PROC
4 Validate invoice: input=vendor clearance, output=payment-ready record, tool=AP Portal, owner=FIN
5 Close project: input=payment-ready record, output=closed CAPEX, tool=ERP, owner=FIN
ระบุ arrows ระหว่าง cell ที่มี handoff จริงเท่านั้น; node ทุกตัวต้องมี IN/OUT chip และ tool
เน้น step 2 เป็น focal step และ node ที่พบ defect เป็น focal nodeได้อย่างละ 1 จุด
ไม่เกิน 6 lanes, 12 steps, ไม่มี diagonal connector และแยก overview/detail หากข้อมูลล้น
ผู้ชม: mixed; ขนาด: slide-16x9; variant: full editorial; format: html
ชื่อไฟล์: capex-handover-process.html
```

#### F. Swimlane — workflow ข้ามทีมแบบอ่านง่าย

ใช้ `swimlane` เมื่อแกนหลักคือ **ใครทำอะไรและส่งต่องานให้ใคร** โดยให้แต่ละ step อยู่ใน lane ของ owner เพียงคนเดียว และวางลำดับให้ลูกศรย้อนกลับน้อยที่สุด

```text
ใช้ diagram-design สร้าง swimlane diagram เรื่อง change request ตั้งแต่แจ้งปัญหาจน deploy
lanes: Requester, Service Desk, Developer, QA, Release Manager
steps ตามลำดับ:
Requester: เปิด ticket
Service Desk: ตรวจข้อมูลและจัด priority
Developer: วิเคราะห์และสร้าง patch
QA: ทดสอบ regression
Release Manager: อนุมัติ release
Developer: deploy ไป staging
QA: ตรวจ smoke test
Release Manager: deploy production และปิด ticket
ทำให้ handoff ระหว่าง Service Desk→Developer และ QA→Release Manager เด่นที่สุด
ทุก step ต้องอยู่ lane เดียว, lane ต้องมี label, ไม่วาดกล่องคร่อมสอง lane,
หลีกเลี่ยงเส้นที่วกกลับ; ใช้ accent ไม่เกิน 2 จุดและ arrows แบบ rounded orthogonal
ผู้ชม: mixed; ขนาด: doc-wide; detail: balanced; variant: minimal light; format: html
ชื่อไฟล์: change-request-swimlane.html
```

#### G. Sankey — ปริมาณที่แยกและรวม

ใช้ `sankey` เมื่อ **ความหนาของ ribbon มีความหมายเป็นปริมาณ** ต้องมี exactly 3 stage columns, ยอดรวมแต่ละ stage ต้องสมดุล และไม่ควรใช้กับลำดับขั้นธรรมดาที่ไม่มีการ split/merge

```text
ใช้ diagram-design สร้าง Sankey diagram แสดงการใช้เวลา CI ของทีมใน 1 เดือน
unit: นาที; scale เดียวกันทั้งภาพ; รวมทั้งหมด 12,000 นาที
column 1 / source: CI budget = 12,000
column 2 / test stage: Unit tests = 5,200; E2E tests = 4,000; Build = 2,000; Lint = 800
column 3 / outcome: Passed = 9,400; Failed = 1,600; Flaked = 1,000
flows:
- CI budget → Unit tests 5,200 → Passed 4,800 / Failed 200 / Flaked 200
- CI budget → E2E tests 4,000 → Passed 3,200 / Failed 500 / Flaked 300
- CI budget → Build 2,000 → Passed 1,700 / Failed 300
- CI budget → Lint 800 → Passed 700 / Failed 100
ตรวจให้ทุก node balance และ ribbon ขั้นต่ำมองเห็นได้; ถ้าเล็กเกิน 4px ให้รวมเป็น Other
จัดลำดับ node เพื่อลด crossing, ใช้ muted กับ flow ปกติ และ accent เฉพาะเส้นทาง Flaked → rerun
ห้าม arrowhead, ห้าม rainbow ต่อ flow, ไม่เกิน 8 nodes และ 12 ribbons
ผู้ชม: engineer; ขนาด: doc-wide; detail: faithful; variant: minimal dark; format: html+png
ชื่อไฟล์: ci-time-sankey.html
```

#### H. Prompt แบบสั้นสำหรับเริ่มต้นเร็ว

```text
สร้าง [radar|gantt|process|swimlane|sankey|fishbone] เรื่อง [หัวข้อ]
เป้าหมาย: [ประโยคเดียวว่าผู้อ่านต้องเข้าใจอะไร]
ข้อมูลจริง: [รายการข้อมูล/วันที่/ปริมาณ/owner]
จุดเน้น: [ไม่เกิน 1–2 จุด]
ผู้ชม: mixed; ขนาด: doc-wide; detail: balanced; variant: minimal light; format: html
ตรวจ type fit, complexity budget, accessibility, 4px grid, connector/ribbon rules และ self-check
ส่งไฟล์ self-contained ชื่อ [slug].html พร้อมสรุป assumption ที่ใช้
```

ก่อนส่ง prompt ให้ตรวจว่า Fishbone มี effect เดียว, Radar ใช้ scale เดียว, Gantt มีวันที่จริง, Process มี input/output/tool, Swimlane มี owner ต่อ step และ Sankey balance ครบทุก column

### 14.2 ภาพตัวอย่างจาก repository

ภาพทั้งหมดด้านล่างเป็น screenshot ที่เก็บอยู่ใน `docs/screenshots/` และอ้างอิงด้วย relative path จึงแสดงผลได้ทั้งใน GitHub และใน preview ของ Markdown ภายใน repository ภาพเป็น **static final frame**; หากต้องการ animation ให้สร้างเป็น HTML แล้วเปิดโหมด `reveal`, `step` หรือ `loop` ตาม prompt ในหัวข้อ 14.1

#### Animation / Loop

![ตัวอย่าง Loop diagram — shared memory และวงจร Capture → Research → Decide → Act → Measure → Learn](docs/screenshots/loop.png)

แหล่งต้นฉบับ: [`example-loop.html`](skills/diagram-design/assets/example-loop.html) · mapping: [`manifest.json`](docs/screenshots/manifest.json)

> ภาพนี้ใช้ดูโครงสร้าง static ของ loop; token ที่เคลื่อนที่เป็น animation ต้องเป็น decorative และต้องไม่เปลี่ยนความหมายของ diagram

#### Fishbone / Ishikawa

![ตัวอย่าง Fishbone diagram — checkout p99 latency และ confirmed root cause](docs/screenshots/fishbone.png)

แหล่งต้นฉบับ: [`example-fishbone.html`](skills/diagram-design/assets/example-fishbone.html) · mapping: [`manifest.json`](docs/screenshots/manifest.json)

> สังเกตว่า effect อยู่ที่หัวปลา, สาเหตุถูกจัดเป็น bone และมี root cause ที่เน้นด้วย accent เพียงหนึ่งกลุ่ม

#### Radar / Spider

![ตัวอย่าง Radar / Spider chart — เปรียบเทียบ storage backends บน 5 criteria](docs/screenshots/radar.png)

แหล่งต้นฉบับ: [`example-radar.html`](skills/diagram-design/assets/example-radar.html) · mapping: [`manifest.json`](docs/screenshots/manifest.json)

> ใช้แกน 5 แกนบน scale เดียวกัน และเน้น series ที่แนะนำด้วย accent พร้อม vertex dots

#### Gantt

![ตัวอย่าง Gantt chart — phase, task, critical gate และช่วงเวลาที่ซ้อนกัน](docs/screenshots/gantt.png)

แหล่งต้นฉบับ: [`example-gantt.html`](skills/diagram-design/assets/example-gantt.html) · mapping: [`manifest.json`](docs/screenshots/manifest.json)

> ใช้แถบงานสำหรับช่วง start/end, แบ่ง phase เป็นโซน และใช้ accent กับ critical gate เพียงจุดหลัก

#### Process

![ตัวอย่าง Process diagram — หลาย actor พร้อม input/output, tool และ data handoff](docs/screenshots/process.png)

แหล่งต้นฉบับ: [`example-process.html`](skills/diagram-design/assets/example-process.html) · mapping: [`manifest.json`](docs/screenshots/manifest.json)

> เหมาะเมื่อแต่ละ step ต้องอ่าน owner, data type และเครื่องมือที่ใช้ได้พร้อมกัน ไม่ใช่แค่ลำดับของงาน

#### Swimlane

![ตัวอย่าง Swimlane diagram — workflow ข้าม Author, Reviewer, Editor และ CI/CD](docs/screenshots/swimlane.png)

แหล่งต้นฉบับ: [`example-swimlane.html`](skills/diagram-design/assets/example-swimlane.html) · mapping: [`manifest.json`](docs/screenshots/manifest.json)

> แต่ละ step อยู่ใน lane ของ owner เดียว และ handoff ข้าม lane เป็นจุดสำคัญของภาพ

#### Sankey

![ตัวอย่าง Sankey diagram — CI minutes แยกเป็น test stages และรวมเป็น outcomes](docs/screenshots/sankey.png)

แหล่งต้นฉบับ: [`example-sankey.html`](skills/diagram-design/assets/example-sankey.html) · mapping: [`manifest.json`](docs/screenshots/manifest.json)

> ความหนาของ ribbon แทนปริมาณจริง, มี 3 stage columns, ไม่มี arrowhead และยอดรวมระหว่าง stage ต้อง balance

## 15. ตำแหน่งไฟล์อ้างอิง

โดยปกติ skill อยู่ที่:

```text
C:\Users\620116\.codex\skills\diagram-design\
```

ไฟล์สำคัญ:

```text
SKILL.md
references\style-guide.md
references\semantic-patterns.md
references\output-spec.md
references\onboarding.md
references\profiles.md
references\import-drawio.md
references\import-mermaid.md
references\export.md
references\doctor.md
references\animation.md
references\type-<ชื่อไดอะแกรม>.md
assets\template.html
assets\template-dark.html
assets\template-full.html
assets\template-motion.html
assets\template-terminal.html
scripts\drawio_extract.py
scripts\mermaid_extract.py
scripts\self_check.py
```

ถ้าคำสั่ง slash ไม่ทำงาน ให้ใช้ prompt ภาษาธรรมชาติในคู่มือนี้แทน และระบุ path ของไฟล์ให้ชัดเจน
