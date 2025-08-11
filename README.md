# FPGA Audio Message Recorder/Player

An FPGA-based **real-time audio recording and playback system** implemented on the Digilent **Anvyl Spartan-6 FPGA board**, integrating a **PicoBlaze soft microcontroller**, **SSM2603 audio codec**, and **DDR2 SDRAM**.

---

## 📹 Demo
[Watch the Demo Video](https://youtu.be/0oZiMBJMgEo)

---

## 📜 Features
- **Record, Play, Delete, and Volume Control** from an interactive UART menu.
- **Real-time recording and playback** with <10 ms latency.
- Stores **≥4 minutes** of variable-length audio messages across ≥5 recordings.
- **Pause/Resume** functionality during playback.
- Multi-clock domain architecture for **DDR2, PicoBlaze, and Audio Codec**.
- Low-level I²C communication for **codec configuration**.
- PicoBlaze assembly for **menu navigation** and UART I/O.

---

## 🛠 Hardware Architecture
**Main Components:**
- **FPGA Board:** Digilent Anvyl Spartan-6 LX45
- **Soft MCU:** PicoBlaze (Xilinx KCPSM6)
- **Audio Codec:** Analog Devices SSM2603
- **Memory:** 1 Gbit onboard DDR2 SDRAM
- **I/O Interfaces:** UART (PuTTY/Serial Terminal), push buttons, LEDs, DIP switches

**Block Diagram:**

---

## 🔧 Design Overview

### 1. **Multi-Clock Domain Integration**
- **37.5 MHz** DDR2 interface clock for memory state machine.
- **100 MHz** for PicoBlaze, UART, and general logic.
- **50 MHz** & **11.2896 MHz** from codec's internal PLL for audio sampling.

### 2. **Audio Recording Path**
- Mic input sampled by codec.
- Data synchronized using `sample_req`/`sample_end` signals.
- Samples written sequentially to DDR2.

### 3. **Audio Playback Path**
- PicoBlaze selects message.
- DDR2 read logic streams samples to codec for speaker output.

### 4. **User Interface**
- UART menu on startup:
