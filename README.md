# 🔐 RFID Secure Access Control System (PIC16F877A)

[![GitHub Repository](https://img.shields.io/badge/GitHub-Repository-00f0ff?style=for-the-badge&logo=github&logoColor=white)](https://github.com/ALWINTR/rfid-access-control-pic16f877a)
[![Developer](https://img.shields.io/badge/Developer-Alwin_T_R-0284c7?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/alwintr)
[![Platform](https://img.shields.io/badge/Platform-PIC16F877A_%26_Proteus-38bdf8?style=for-the-badge&logo=microchip&logoColor=white)](https://github.com/ALWINTR)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

An industrial-grade embedded credential verification and secure access control system powered by the **Microchip PIC16F877A** 8-bit microcontroller, featuring 13.56MHz SPI RFID card validation, alphanumeric 16x2 LCD status display, relay/servo electronic door strike lock actuation, and a complete Proteus VSM simulation model.

---

## 📌 System Architecture

```
       ┌──────────────────────────────┐
       │  MFRC522 13.56MHz RFID Card  │
       └──────────────┬───────────────┘
                      │ SPI Bus (SCK, SDI, SDO, CS)
                      ▼
       ┌──────────────────────────────┐
       │   PIC16F877A Microcontroller │
       │   • MSSP SPI Module          │
       │   • Internal EEPROM Match    │
       └──┬────────────────────────┬──┘
          │ 8-Bit Parallel Bus     │ Relay / Lock Pulse
          ▼                        ▼
  ┌───────────────┐        ┌───────────────┐
  │ 16x2 HD44780  │        │ Relay & Door  │
  │ Character LCD │        │ Strike Lock   │
  └───────────────┘        └───────────────┘
```

---

## ⚙️ Hardware Components & Technical Specifications

| Component | Technical Specification | Function |
| :--- | :--- | :--- |
| **Microcontroller** | Microchip PIC16F877A (20MHz Crystal) | 8KB Flash, 368B RAM, 256B EEPROM |
| **RFID Reader** | MFRC522 (13.56MHz SPI Transceiver) | Contactless ISO/IEC 14443A card reader |
| **Visual Display** | 16x2 HD44780 Alphanumeric LCD | Real-time user greeting & access status |
| **Lock Actuator** | 5V Single-Channel Relay / SG90 Servo | High-current solenoid door strike driver |
| **Audio Feedback** | 5V Active Piezo Buzzer | Success beep (1x) vs Denial siren (3x) |
| **Simulation Suite** | Proteus VSM (.pdsprj) | Full hardware validation in circuit simulator |

---

## 🔌 PIC16F877A Pinout & Memory Mapping

| PIC16F877A Pin | Port / Register | Connected Peripheral | Description |
| :--- | :--- | :--- | :--- |
| **Pin 13 / 14** | OSC1 / OSC2 | 20MHz Crystal + 22pF Caps | Master system clock oscillator |
| **Pin 1 (MCLR)** | RE3 / MCLR | 10kΩ Pull-up Resistor | Hardware master clear reset |
| **Pin 18 (RC3)** | SCK (MSSP) | RC522 SPI SCK | Master Synchronous Serial Clock |
| **Pin 23 (RC4)** | SDI (MSSP) | RC522 SPI MISO (SDO) | Master Serial Data In |
| **Pin 24 (RC5)** | SDO (MSSP) | RC522 SPI MOSI (SDI) | Master Serial Data Out |
| **Pin 2 (RA0)** | RA0 (Digital Out) | RC522 SDA (Chip Select) | Slave Select Active LOW |
| **Pins 19-22, 27-30** | PORTD (RD0-RD7) | 16x2 LCD Data Bus | 8-Bit parallel character transfer |
| **Pin 33 (RB0)** | RB0 / INT | Lock Relay Driver Transistor | Active HIGH door unlock pulse |
| **Pin 34 (RB1)** | RB1 (Digital Out) | Status Buzzer Driver | Audio feedback tone generator |

---

## 🧠 Firmware Architecture & Verification Routine

The firmware (`firmware/main.c`) is written in ANSI Embedded C for the Microchip XC8 compiler:
1. **SPI Master Initialization**: Configures MSSP control registers (`SSPCON`, `SSPSTAT`) for SPI Mode 0,0 at \( F_{OSC}/4 \).
2. **RFID Polling & Card Anti-Collision**: Detects tag presence, executes cascade level 1 anti-collision, and retrieves the 4-byte / 7-byte Unique Identifier (UID).
3. **EEPROM Whitelist Lookup**: Compares scanned UID against authorized key cards stored in non-volatile internal EEPROM memory.
4. **Access Decisions**:
   - **AUTHORIZED**: Displays `"Access Granted: ALWIN"`, triggers relay for 5 seconds, emits confirmation beep.
   - **UNAUTHORIZED**: Displays `"Access Denied!"`, flashes alert indicator, logs access attempt.

---

## 🖥️ Proteus Simulation Guide

1. Open Proteus VSM (version 8.9 or higher).
2. Navigate to `proteus/` folder and load `rfid_access_control.pdsprj`.
3. Right-click the **PIC16F877A** component -> Edit Properties.
4. Point **Program File** to the compiled `.hex` binary in `firmware/dist/`.
5. Set Clock Frequency to **20MHz**.
6. Press **Play** to run interactive simulation with animated LCD and relay actuation.

---

## 👨‍💻 Author

**Alwin T R** — Robotics & Automation Engineer  
- 💼 LinkedIn: [linkedin.com/in/alwintr](https://www.linkedin.com/in/alwintr)  
- 🌌 Portfolio: [alwintr.github.io](https://alwintr.github.io)  
- 💻 GitHub: [github.com/ALWINTR](https://github.com/ALWINTR)

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.
