# **Audio-Based Authentication System for Access Control using Boolean FPGA**

This project implements a secure, touchless access control system using **voice-based authentication** on a **Boolean FPGA (Spartan-6)**. It combines **Python-generated audio** and **Verilog-based FPGA design** to analyze and compare dominant audio frequencies, allowing access only when the voice patterns match.

---

## 🚀 **Project Overview**

- **Technology**: Spartan-6 FPGA (Boolean Board), Verilog HDL, Python (gTTS, pydub), Vivado Design Suite  
- **Function**: Uses FFT-based frequency analysis to compare a test voice against a stored reference and activates a servo motor if they match (simulates door unlock).  
- **Applications**: Smart home access, secure labs, voice-based authentication systems

---

## 🎯 **System Workflow**

### 🔉 Audio Generation (Python)
- Generates speech using **Google Text-to-Speech (gTTS)**
- Converts audio to **16-bit PCM** and saves as `.mem` format

### 🔄 Data Transfer (Python UART)
- Sends chunks via **serial** to FPGA
- Command protocol:
  - `'R'` → Reference
  - `'T'` → Test
  - `'D'` → Display/Compare

### 🧠 FPGA Processing (Verilog)
- Stores `.mem` data into **BRAM**
- Simulates **FFT** by finding peak amplitude
- Compares frequencies within a **5% error margin**
- Controls **LEDs and Servo PWM** based on result

### 🟢 Servo Behavior
- ✅ **Match**: `90°` (Unlocked) → All LEDs **ON**  
- ❌ **Mismatch**: `0°` (Locked) → All LEDs **OFF**

---

## 🧠 **Key Modules**

- `uart_rx.v`: UART receiver  
- `uart_bram_led_servo.v`: Main FSM, BRAM, FFT-mock logic, PWM generation  
- `servo_pwm.v`: PWM signal for SG90 servo control  
- `fft_freq_compare.v`: (optional advanced) frequency bin comparison

---

## 💻 **Tools Used**

- **Vivado Design Suite 2024.1** (Synthesis, Simulation, Implementation)
- **Python**: `gTTS`, `pydub`, `numpy`, `pyserial`
- **Hardware**: Boolean FPGA (Spartan-6), SG90 servo, USB-to-UART cable
