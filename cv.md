# SAIKAT KHAN

**Computer Science & Engineering Student | Robotics Enthusiast**

**LinkedIn:** [linkedin.com/in/saikat-k-612186324](https://www.linkedin.com/in/saikat-k-612186324) | **Github:** [github.com/Saikat-dot678](https://github.com/Saikat-dot678)

**Email:** saikatkhan2005saikat@gmail.com | **Phone:** +91 9907813521

---

## EDUCATION

| Degree | School | Year | Grade |
| :--- | :--- | :--- | :--- |
| B.Tech - Computer Science & Engineering | National Institute of Technology Durgapur | 2024 - 2028 | Sem 1: 8.91, Sem 2: 9.12 |
| Class 12 (WBCHSE) | Bishnupur High School | 2022 - 2024 | 462/500 |
| Class 10 (WBBSE) | Bishnupur High School | 2020 - 2022 | 678/700 |

---

## TECHNICAL SKILLS

* **Programming:** C, C++, Python, Rust, JavaScript, HTML, CSS
* **Hardware:** Raspberry Pi 5, ESP32-S3, SX1262 LoRa Modules, Sensors (IMU, Ultrasonic)
* **Frameworks & Libraries:** ROS2 (Humble), OpenCV, PyTorch, Node.js, Express.js, MediaPipe
* **Databases:** MySQL, PostgreSQL, MongoDB
* **Protocols & Networking:** LoRaWAN, MQTT, SPI/I2C/UART, Selective Repeat ARQ, TCP/IP Basics

---

## PROJECTS

### 1. Sohojia Foundation Monitoring System (Full-Stack & AI)
*Node.js, Python, InsightFace, MySQL, MongoDB, Docker, Google Cloud*
* **Architected a hybrid microservice system** to automate volunteer monitoring for a rural education NGO, replacing manual oversight with a secure web-based platform.
* **Implemented Multi-Factor Attendance:** Engineered a verification pipeline using **GPS Geofencing** (100m radius) and **Face Verification** via a Python microservice (InsightFace buffalo_l model).
* **Developed Secure RBAC:** Built a hierarchical Role-Based Access Control system using **HttpOnly JWT cookies** and bcrypt hashing to manage Admin, Director, and Volunteer permissions.
* **Cloud & Automation:** Integrated Google Cloud Storage for biometric data and established **Automated Cron Jobs** for real-time lateness tracking and absence reporting.

### 2. Pose-Controlled Game Interface (Computer Vision & HCI)
*Python, OpenCV, MediaPipe, PyAutoGUI*
* **Engineered a touchless gaming interface** that translates real-time human body gestures into keyboard commands using **MediaPipe Pose Estimation**.
* **Developed Gesture Mapping Logic:** Programmed algorithms to detect horizontal/vertical shoulder displacement for movement (Left/Right/Jump/Crouch) and hand-distance thresholds for "Clap to Start" triggers.
* **Optimized Input Response:** Utilized **PyAutoGUI** for low-latency simulation of keyboard events, enabling real-time control of third-party applications and games.

### 3. LoRa Mesh Communication System (Embedded Systems & Networking)
*ESP32-S3, Dual SX1262, Python/C++, SPI, Selective Repeat ARQ*
* [cite_start]**Developed a decentralized Long Range (LoRa) protocol** v1.2 featuring a **Reliable Transport Layer** to ensure data integrity over long-distance, high-interference links[cite: 1].
* **Designed Dual-Radio Full-Duplex Emulation:** Configured a dual SX1262 hardware architecture where one radio is dedicated to continuous RX and the other to TX/CAD to eliminate communication "blind spots".
* **Implemented Advanced Reliability:** Built a custom networking stack including **Selective Repeat ARQ**, packet fragmentation, and CRC16-CCITT checksums to mitigate packet loss at Spreading Factor 12 (SF12).
* **Engineered Collision Avoidance:** Integrated a **Listen Before Talk (LBT)** algorithm with random backoff and Channel Activity Detection (CAD) to manage medium access in congested mesh environments.

---
