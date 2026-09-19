# RFID Secure Access Control and Authentication System (PIC16F877A)

[![GitHub Repository](https://img.shields.io/badge/GitHub-Repository-00f0ff?style=for-the-badge&logo=github&logoColor=white)](https://github.com/ALWINTR/RFID-Secure-Access-Control-and-Authentication-System-PIC16F877A)
[![Developer](https://img.shields.io/badge/Developer-Alwin_T_R-0284c7?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/alwintr)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

An industrial-grade embedded credential verification and secure access control system powered by the **Microchip PIC16F877A** 8-bit microcontroller, featuring 13.56MHz SPI RFID card validation, alphanumeric 16x2 LCD status display, relay/servo electronic door strike lock actuation, and a complete Proteus VSM simulation model.

---

## System Architecture

```
       +------------------------------+
       |  MFRC522 13.56MHz RFID Card  |
       +--------------+---------------+
                      | SPI Bus (SCK, SDI, SDO, CS)
                      v
       +------------------------------+
       |   PIC16F877A Microcontroller |
       |   - MSSP SPI Module          |
       |   - Internal EEPROM Match    |
       +--+------------------------+--+
          | 8-Bit Parallel Bus     | Relay / Lock Pulse
          v                        v
  +---------------+        +---------------+
  | 16x2 HD44780  |        | Relay & Door  |
  | Character LCD |        | Strike Lock   |
  +---------------+        +---------------+
```

---

## Hardware Bill of Materials (BOM)

| Component | Technical Specification | Functional Role |
| :--- | :--- | :--- |
| **Microcontroller** | Microchip PIC16F877A (20MHz Crystal) | 8KB Flash, 368B RAM, 256B EEPROM |
| **RFID Reader** | MFRC522 (13.56MHz SPI Transceiver) | Contactless ISO/IEC 14443A card verification |
| **Visual Display** | 16x2 HD44780 Alphanumeric LCD | User authentication feedback and system status |
| **Lock Actuator** | 5V Single-Channel Relay / Servo | High-current solenoid door strike driver |
| **Audio Feedback** | 5V Active Piezo Buzzer | Success beep (1x) vs Denial siren (3x) |
| **Simulation Model**| Proteus VSM (.pdsprj) | Full hardware simulation and validation suite |

---

## Circuit Pinout Table

| PIC16F877A Pin | Port / Register | Connected Peripheral | Description |
| :--- | :--- | :--- | :--- |
| **Pin 13 / 14** | OSC1 / OSC2 | 20MHz Crystal with 22pF Caps | Master system clock oscillator |
| **Pin 1 (MCLR)** | RE3 / MCLR | 10k Pull-up Resistor | Hardware master clear reset |
| **Pin 18 (RC3)** | SCK (MSSP) | RC522 SPI SCK | Master Synchronous Serial Clock |
| **Pin 23 (RC4)** | SDI (MSSP) | RC522 SPI MISO (SDO) | Master Serial Data In |
| **Pin 24 (RC5)** | SDO (MSSP) | RC522 SPI MOSI (SDI) | Master Serial Data Out |
| **Pin 2 (RA0)** | RA0 (Digital Out) | RC522 SDA (Chip Select) | Slave Select Active LOW |
| **Pins 19-22, 27-30** | PORTD (RD0-RD7) | 16x2 LCD Data Bus | 8-Bit parallel character transfer |
| **Pin 33 (RB0)** | RB0 / INT | Lock Relay Driver | Active HIGH door unlock pulse |
| **Pin 34 (RB1)** | RB1 (Digital Out) | Status Buzzer Driver | Audio feedback tone generator |

---

## Proteus Simulation Instructions

1. Launch Proteus VSM (version 8.9 or higher).
2. Open `proteus/rfid_access_control.pdsprj`.
3. Right-click the **PIC16F877A** component -> Edit Properties.
4. Point **Program File** to the compiled `.hex` binary in `firmware/dist/`.
5. Set Clock Frequency to **20MHz**.
6. Press **Play** to run interactive simulation with animated LCD and relay actuation.

---

## Author

**Alwin T R** - Robotics and Automation Engineer  
- LinkedIn: [linkedin.com/in/alwintr](https://www.linkedin.com/in/alwintr)  
- Portfolio: [alwintr.github.io](https://alwintr.github.io)  
- GitHub: [github.com/ALWINTR](https://github.com/ALWINTR)

---

## License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.
