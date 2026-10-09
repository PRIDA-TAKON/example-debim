# Example debim (Building-as-Code)

แบบจำลองบ้านตัวอย่าง: **แบบบ้านไทยอนุรักษ์ ภาคอีสาน (มบ. 462105)**  
พัฒนาด้วย [debim](https://github.com/PRIDA-TAKON/debim) (Declarative BIM Compiler)

## 📁 ไฟล์ใน Repository

- `project.debim` — โค้ดโมเดลอาคารแบบ Declarative YAML (โครงสร้าง เสา คาน พื้น ผนัง ประตู-หน้าต่าง หลังคา สุขภัณฑ์)
- `viewer.html` — Standalone 3D Web Viewer (เปิดดูโมเดล 3 มิติได้ทันทีบนเว็บเบราว์เซอร์ ไม่ต้องลงโปรแกรม)
- `viewer_2d.html` — Interactive 2D Blueprint Viewer (แปลนสถาปัตย์ 2 มิติ พร้อมเครื่องมือวัดระยะ Pan-Zoom)
- `prices.yaml` — บัญชีราคาค่าวัสดุและค่าแรงมาตรฐาน (อ้างอิง DPT BOQ)
- `boq_breakdown.csv` — รายการสรุปถอดปริมาณและราคาก่อสร้าง (BOQ / QTO Summary)
- `specifications.md` — รายการประกอบแบบสถาปัตยกรรมและวิศวกรรมโครงสร้าง (Architectural Specification Book อ้างอิง CSI MasterFormat 10 หมวดงาน และมาตรฐาน สถ./วสท./มอก.)

## 🚀 คำสั่ง debim ที่เกี่ยวข้อง

```bash
# ตรวจสอบความถูกต้องและกฎหมายควบคุมอาคาร
debim validate -m project.debim
debim test -m project.debim

# จัดทำรายการประกอบแบบ (Architectural Specifications Book)
debim spec build -m project.debim -s specs/ -o specifications.md

# ถอดปริมาณงาน (Quantitative Take-Off: Concrete, Formwork, Steel)
debim qto -m project.debim

# ประมาณราคาก่อสร้าง (Cost Estimation / BOQ)
debim cost -m project.debim -p prices.yaml --csv boq_breakdown.csv

# สร้าง 3D Web Viewer
debim view -m project.debim --export viewer.html

# สร้าง 2D Blueprint Web Viewer
debim draw view -m project.debim -o viewer_2d.html

# คอมไพล์เป็น IFC4 สำหรับโปรแกรม BIM สากล (BlenderBIM, Revit, FreeCAD)
debim compile -m project.debim -o model.ifc
```
