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

## เครื่องมือที่จำเป็น
- Ubuntu 24.04
- Qt 6.4
- opencv 4.7 ขึ้นไป

## 🛠️ ขั้นตอนที่ 1: เตรียมเครื่องมือพื้นฐาน (Development Tools)

เปิด Terminal ใน Ubuntu (WSL) แล้วรันคำสั่งเพื่อลงเครื่องมือคอมไพล์มาตรฐาน:

* **อัปเดตระบบ:**
    ```bash
    sudo apt update && sudo apt upgrade -y
    ```

* **ติดตั้ง Build Tools:**
    ```bash
    sudo apt install -y build-essential cmake git pkg-config
    ```

* **ติดตั้ง Library พื้นฐาน:**
    ```bash
    sudo apt install -y libxkbcommon-x11-0 libxcb-cursor0
    ```

---

## 📦 ขั้นตอนที่ 2: ติดตั้ง Library หลัก (Dependencies)

อ้างอิงจากไฟล์ `CMakeLists.txt` โปรแกรมนี้ต้องการ **Qt6** และ **OpenCV** ครับ:

* **ติดตั้ง Qt6:**
    ```bash
    sudo apt install -y qt6-base-dev qt6-base-private-dev qt6-tools-dev qt6-tools-dev-tools libqt6opengl6-dev
    ```

* **ติดตั้ง OpenCV:**
    ```bash
    sudo apt install -y libopencv-dev
    ```

* **ติดตั้ง QtMqtt (ต้องบิลด์เอง):**
    ```bash
    git clone https://github.com/qt/qtmqtt.git -b 6.4.2
    cd qtmqtt && mkdir build && cd build
    cmake .. -DQT_NO_PACKAGE_VERSION_CHECK=TRUE
    make -j$(nproc) && sudo make install
    ```
    !!! tip "เวอร์ชันของ QtMqtt"
        คุณสามารถเปลี่ยน `-b 6.4.2` ในคำสั่งด้านบนให้ตรงกับเวอร์ชันของ Qt ที่ติดตั้งอยู่ในเครื่องของคุณได้

---

## 📂 ขั้นตอนที่ 3: การดึงโค้ดโปรเจกต์ (Cloning)

เพื่อให้ได้โค้ดครบทุกส่วนรวมถึง *NodeEditor* และ *Plugins*:

* **Clone แบบรวม Submodules:**
    ```bash
    cd
    git clone --recursive https://github.com/pbunnun/SeeWeDev.git
    cd SeeWeDev
    ```

!!! warning "การยืนยันตัวตนบน GitHub"
    หาก GitHub ถาม Password ระหว่างการ Clone ให้ใช้ **Personal Access Token (PAT)** ที่คุณสร้างไว้ในการยืนยันตัวตนแทนรหัสผ่านปกติ

---

## 🔧 ขั้นตอนที่ 4: การปรับจูนโค้ด (Compatibility Patch)

เนื่องจาก OpenCV ใน Ubuntu 24.04 เป็นรุ่น 4.6 แต่โค้ดบางส่วนเรียกหาฟีเจอร์ของ 4.7+ ต้องรันคำสั่งซ่อมแซมดังนี้:

* **ซ่อม Path ของ ArUco:**
    ```bash
    find . -type f \( -name "*.cpp" -o -name "*.hpp" \) -exec sed -i 's/opencv2\/objdetect\/aruco/opencv2\/aruco/g' {} +
    ```

* **ซ่อม CharucoDetector (วิธีแก้ถาวรด้วย `#if`):** ใช้วิธีครอบโค้ดด้วยคำสั่ง Preprocessor ของ C++:
    ```cpp
    #if CV_VERSION_GREATER_THAN 
    ```

---

## 🚀 ขั้นตอนที่ 5: การบิลด์และรัน (Build & Run)

แนะนำให้บิลด์บน **Drive D** เพื่อประหยัดพื้นที่และแยกไฟล์ระบบออกจากไฟล์งาน:

1. **สร้างโฟลเดอร์บิลด์:**
    ```bash
    mkdir build
    cd build
    ```

2. **ตั้งค่า CMake:**
    ```bash
    cmake ..
    ```

3. **คอมไพล์:**
    ```bash
    make -j$(nproc)
    ```

4. **เปิดโปรแกรม:**
    ```bash
    cd CVDev
    ./CVDev
    ```

## การสร้างแพ็กเกจติดตั้ง (Packaging - Option)
หากต้องการสร้างไฟล์ติดตั้ง .deb สำหรับนำไปใช้กับเครื่อง Ubuntu เครื่องอื่น สามารถใช้คำสั่ง CPack:

    cpack -G DEB

!!! Note 
    - Qt Version: โปรเจกต์นี้รองรับ Qt6.4 เป็นหลัก (ตามที่ระบุใน CPACK_DEBIAN_RUNTIME_PACKAGE_DEPENDS)
    - OpenCV Version: แนะนำให้ใช้ OpenCV 4.7 ขึ้นไป

!!! ไม่ต้องตกใจ
    ถ้าโหนด ROI และ CVCamaracaribase ขึ้น error
