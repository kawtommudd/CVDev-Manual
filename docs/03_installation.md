# การติดตั้งโปรแกรม CVDev

บทนี้อธิบายขั้นตอนและข้อกำหนดในการติดตั้งโปรแกรม CVDev  
โดยอ้างอิงจากเอกสาร INSTALL.md และ README.md ที่ผู้พัฒนาโครงการจัดเตรียมไว้  
เพื่อให้ผู้ใช้งานสามารถเตรียมสภาพแวดล้อมและติดตั้งโปรแกรมได้อย่างถูกต้อง

---

## ความต้องการของระบบ (System Requirements)

โปรแกรม CVDev พัฒนาด้วยภาษา C++ และใช้ไลบรารีหลัก ได้แก่ Qt, OpenCV และ NodeEditor  
ก่อนทำการติดตั้ง จำเป็นต้องเตรียมสภาพแวดล้อมให้เหมาะสมกับระบบปฏิบัติการที่ใช้งาน

ระบบปฏิบัติการที่รองรับ ได้แก่
- Microsoft Windows (64-bit)
- macOS
- Linux (Ubuntu 24.04)
- Raspberry Pi OS (64-bit)

---

## การติดตั้งบนระบบ Windows

### เครื่องมือที่จำเป็น
- Windows 10 หรือ Windows 11 (64-bit)
- Microsoft Visual Studio (2017, 2019 หรือ 2022)
- Qt (เวอร์ชันที่รองรับกับ Visual Studio)
- OpenCV (เวอร์ชัน 4.x)
- vcpkg สำหรับจัดการไลบรารีเพิ่มเติม

ในการคอมไพล์โปรแกรม จำเป็นต้องตั้งค่า CMake ให้ใช้งานร่วมกับ vcpkg  
เพื่อให้ระบบสามารถเรียกใช้ไลบรารีที่ติดตั้งไว้ได้อย่างถูกต้อง

---

## การติดตั้งบนระบบ macOS

### เครื่องมือที่จำเป็น
- macOS เวอร์ชัน 10.15.5 หรือใหม่กว่า
- Homebrew
- Qt เวอร์ชัน 5.15.x
- OpenCV เวอร์ชัน 4.x

ก่อนทำการรันโปรแกรมผ่าน Qt Creator  
ควรตรวจสอบและลบ library search path ที่ไม่จำเป็นในส่วน Run Configuration  
เพื่อป้องกันปัญหาในการโหลดไลบรารีขณะรันโปรแกรม

---

## การติดตั้งบนระบบ Linux (Ubuntu)

## 1. การเตรียมสภาพแวดล้อม (Prerequisites)
ก่อนเริ่มติดตั้ง ต้องติดตั้งเครื่องมือในการ Build และ Library พื้นฐานที่จำเป็นผ่าน Terminal:

    # อัปเดตรายการแพ็กเกจ
    sudo apt update && sudo apt upgrade -y

    # ติดตั้งเครื่องมือ Build พื้นฐาน
    sudo apt install -y build-essential cmake git pkg-config

    # ติดตั้ง Qt6 Development Libraries
    sudo apt install -y qt6-base-dev qt6-base-dev-tools qt6-tools-dev \
    qt6-tools-dev-tools libqt6widgets6 libqt6gui6 libqt6core6

    # ติดตั้ง OpenCV Development Library
    sudo apt install -y libopencv-dev

## 2. การดาวน์โหลดซอร์สโค้ด (Clone Project)
ทำการดึงซอร์สโค้ดหลักและโปรเจกต์ย่อย (Submodules) ที่จำเป็นทั้งหมด:

    # Clone โปรเจกต์จาก GitHub
    git clone https://github.com/pbunnun/SeeWeDev.git
    cd SeeWeDev

    # ตรวจสอบว่าอยู่บนสาขาหลัก (main)
    git checkout main

    # ดึงข้อมูล Submodules (NodeEditor, QtPropertyBrowserLibrary)
    git submodule update --init --recursive

## 3. ขั้นตอนการบิ้วโปรแกรม (Build Process)
เนื่องจากโปรเจกต์ไม่อนุญาตให้ Build ในโฟลเดอร์ซอร์สโค้ดโดยตรง (In-source build disabled) จึงต้องสร้างโฟลเดอร์ build แยกต่างหาก:

    # สร้างและเข้าโฟลเดอร์สำหรับ Build
    mkdir build
    cd build

    # กำหนดค่าโปรเจกต์ด้วย CMake
    cmake ..

    # เริ่มการคอมไพล์โปรแกรม
    make -j4

## 4. การรันโปรแกรม (Execution)
เมื่อกระบวนการบิ้วเสร็จสิ้น 100% คุณจะพบไฟล์รันหลักอยู่ในโฟลเดอร์ย่อยภายใน build (โดยปกติจะอยู่ใน build/Main/ หรือตามโครงสร้างที่ CMake กำหนด):

    # ตัวอย่างการรันโปรแกรม
    ./Main/CVDev

## 5. การสร้างแพ็กเกจติดตั้ง (Packaging - Option)
หากต้องการสร้างไฟล์ติดตั้ง .deb สำหรับนำไปใช้กับเครื่อง Ubuntu เครื่องอื่น สามารถใช้คำสั่ง CPack:

    cpack -G DEB

!!! Note 
    - Qt Version: โปรเจกต์นี้รองรับ Qt6 เป็นหลัก (ตามที่ระบุใน CPACK_DEBIAN_RUNTIME_PACKAGE_DEPENDS)
    - OpenCV Version: แนะนำให้ใช้ OpenCV 4.x ขึ้นไป
