# ภาพรวมส่วนติดต่อผู้ใช้ (UI Overview)

บทนี้อธิบายภาพรวมของส่วนติดต่อผู้ใช้ (User Interface) ของโปรแกรม CVDev เพื่อให้ผู้ใช้งานเข้าใจโครงสร้างหน้าจอและหน้าที่ของแต่ละส่วนก่อนเริ่มใช้งานจริง

---

## หน้าจอหลักของโปรแกรม
![หน้าจอหลักของโปรแกรม CVDev](images/ui/screen.png)

เมื่อเปิดโปรแกรม CVDev ผู้ใช้งานจะพบกับหน้าจอหลักซึ่งประกอบด้วยสี่สส่วน คือ แถบเมนู (Menu Bar) แผงโหนด (Node Panel) พื้นที่แสดงผลลัพธ์ (Output Panel) พื้นที่ทำงาน (Workspace) แผงคุณสมบัติ (Property Panel)

---

## แถบเมนู (Menu Bar)
<p align="center">
	<img src="../images/ui/toolbar.png" alt="แถบเมนู CVDev">
</p>

แถบเมนูอยู่บริเวณด้านบนของหน้าจอ ใช้สำหรับจัดการโปรเจกต์และการตั้งค่าระบบ เช่น

* <img src="../images/icons/new_project.png" width="35" style="vertical-align: middle;"> สร้างโปรเจกต์ใหม่ (New Project) สร้างพื้นที่ทำงานใหม่ / ล้างหน้าจอ
* <img src="../images/icons/load.png" width="35" style="vertical-align: middle;"> เปิดไฟล์งาน (Load หรือ Open File) เรียกดูและเปิดไฟล์โปรเจกต์เดิมที่เคยบันทึกไว้ขึ้นมา เพื่อทำการแก้ไขหรือใช้งานต่อ
* <img src="../images/icons/save.png" width="35" style="vertical-align: middle;"> บันทึกโปรเจค (Save Projec) บันทึกการเปลี่ยนแปลงล่าสุดลงในไฟล์โปรเจกต์
* <img src="../images/icons/undo.png" width="35" style="vertical-align: middle;"> ยกเลิกสิ่งที่ทำไปแล้ว (Undo) ย้อนกลับไปสถานะก่อนหน้า หรือยกเลิกคำสั่งล่าสุดที่เพิ่งทำไป (เช่น กรณีลบโหนดผิด หรือลากวางผิดตำแหน่ง)
* <img src="../images/icons/redo.png" width="35" style="vertical-align: middle;"> การทำซ้ำ(Redo) ย้อนกลับการกระทำที่เพิ่งถูกยกเลิกไป (ใช้สำหรับกู้คืนสิ่งที่เพิ่งกด Undo ไป)
* <img src="../images/icons/snap to grid.png" width="35" style="vertical-align: middle;"> การจัดแนวตามเส้นตาราง (Snap to grid) ช่วยจัดตำแหน่งของโหนดให้ตรงกับเส้นตารางโดยอัตโนมัติเมื่อทำการเคลื่อนย้าย เพื่อให้ผังงานดูเป็นระเบียบ
---

## แผงโหนด (Node Panel)
<p align="center">
        <img src="../images/ui/node.png" alt="แผงโหนด CVDev">
</p>

แผงโหนดแสดงรายการโหนดที่สามารถใช้งานได้ 
ผู้ใช้งานสามารถเลือกโหนดที่ต้องการและเพิ่มลงใน Workflow ได้อย่างง่ายดาย

---
## พื้นที่แสดงผลลัพธ์ (Output Panel)
![หน้าจอหลักแสดงผล CVDev](images/ui/output.png)

พื้นที่แสดงผลลัพธ์ใช้สำหรับแสดงผลลัพธ์จากการประมวลผล
เช่น ภาพที่ผ่านการประมวลผล หรือผลลัพธ์จากโมเดล Machine Learning

---

## พื้นที่ทำงาน (Workspace)
<p align="center">
        <img src="../images/ui/workspace.png" alt="พื้นที่ทำงาน CVDev">
</p>

พื้นที่ทำงานหรือ Canvas เป็นบริเวณหลักสำหรับสร้าง Workflow
ผู้ใช้งานสามารถลากโหนดจากแผงโหนดมาวางและเชื่อมต่อกันในบริเวณนี้

---

## แผงคุณสมบัติ (Property Panel)
<p align="center">
        <img src="../images/ui/proper.png" alt="แผงคุณสมบัติ CVDev">
</p>

แผงคุณสมบัติใช้สำหรับปรับค่าพารามิเตอร์ของโหนดที่เลือก
เช่น ขนาดภาพ ค่า Threshold หรือพาธของไฟล์อินพุต

---


