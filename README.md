# Example debim (Building-as-Code)

โมเดลอาคารตัวอย่างสำหรับ **debim** (Declarative BIM / Building-as-Code Compiler): **แบบบ้านไทยอนุรักษ์ไทย ภาคอีสาน (แบบเลขที่ ม.บ. 462105)**

---

## 🏛️ ที่มาของแบบและคณะผู้รับรองแบบ (Design Provenance & Certifications)

แบบบ้านหลังนี้เป็น **แบบบ้านมาตรฐานแจกฟรีแก่ประชาชน** ภายใต้โครงการแบบอาคารเพื่อประชาชน โดยรัฐบาลมีนโยบายบริการประชาชนโดยไม่คิดค่าบริการออกแบบใดๆ ทั้งสิ้น เพื่อให้ประชาชนนำไปยื่นขออนุญาตปลูกสร้างบ้านพักอาศัยที่ถูกต้องตามมาตรฐานวิศวกรรมและสถาปัตยกรรมไทย

- **หน่วยงานเจ้าของแบบและแจกจ่าย:** **กรมโยธาธิการและผังเมือง กระทรวงมหาดไทย** (Department of Public Works and Town & Country Planning - DPT)
- **ชื่อโครงการ:** โครงการแบบอาคารเพื่อประชาชน "ไทยอนุรักษ์ไทย"
- **ชื่อแบบ:** แบบบ้านไทยอนุรักษ์ไทย ภาคอีสาน
- **เลขที่แบบมาตรฐาน:** **ม.บ. 462105** (อนุมัติแบบเมื่อวันที่ 21 พฤศจิกายน 2546)
- **ผู้อนุมัติแบบ:** **นายสว่าง ศรีสกุน** (อธิบดีกรมโยธาธิการและผังเมือง)
- **สถาปนิกผู้ออกแบบและรับรองแบบ:** **สำนักสถาปัตยกรรม กรมโยธาธิการและผังเมือง**
  - ควบคุมและรับรองแบบสถาปัตยกรรมตามพระราชบัญญัติควบคุมอาคาร พ.ศ. 2522
- **วิศวกรผู้ออกแบบและรับรองแบบ:** **สำนักวิศวกรรมโครงสร้างและงานระบบ กรมโยธาธิการและผังเมือง**
  - **วิศวกรรมโครงสร้าง:** รับรองรายการคำนวณและแบบขยายคอนกรีตเสริมเหล็กและโครงหลังคาเหล็กรูปพรรณ ตามมาตรฐาน มยธ. 101 - มยธ. 106 และ วสท.
  - **วิศวกรรมไฟฟ้าและเครื่องกล:** รับรองระบบไฟฟ้ากำลัง แสงสว่าง และความปลอดภัยตามมาตรฐาน กฟน./กฟภ. และ วสท.
  - **วิศวกรรมสุขาภิบาล:** รับรองระบบท่อประปา ท่อระบายน้ำทิ้ง น้ำเสีย และการบำบัดสิ่งปฏิกูลตามมาตรฐานสุขาภิบาลสากล

---

## 📁 ไฟล์ใน Repository

| ไฟล์ | รายละเอียด |
|---|---|
| [`project.debim`](project.debim) | โค้ดโมเดลอาคารแบบ Declarative YAML (โครงสร้าง เสา คาน พื้น ผนัง ประตู-หน้าต่าง หลังคา สุขภัณฑ์) |
| [`viewer.html`](viewer.html) | Standalone 3D Web Viewer (เปิดดูโมเดล 3 มิติได้ทันทีบนเว็บเบราว์เซอร์ ไม่ต้องติดตั้งโปรแกรม) |
| [`viewer_2d.html`](viewer_2d.html) | Interactive 2D Blueprint Viewer (แปลนสถาปัตย์ 2 มิติ พร้อมเครื่องมือวัดระยะ Pan-Zoom) |
| [`prices.yaml`](prices.yaml) | บัญชีราคาค่าวัสดุและค่าแรงมาตรฐาน (อ้างอิง DPT BOQ 409 รายการ) |
| [`boq_breakdown.csv`](boq_breakdown.csv) | รายการสรุปถอดปริมาณและราคาก่อสร้าง (BOQ / QTO Summary) |
| [`specifications.md`](specifications.md) | รายการประกอบแบบสถาปัตยกรรมและวิศวกรรมโครงสร้าง (Architectural Specification Book อ้างอิง CSI MasterFormat 10 หมวดงาน และมาตรฐาน สถ./วสท./มอก.) |

---

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
