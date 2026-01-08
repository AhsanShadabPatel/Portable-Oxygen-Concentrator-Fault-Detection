# 🫁 Portable Oxygen Concentrator with Fault Detection

## 📌 Overview
This project presents the design and implementation of a **portable oxygen concentrator based on Pressure Swing Adsorption (PSA)** combined with an **oxygen analyzer and fault detection system**. The system is intended for **medical and emergency use**, especially in regions with limited access to oxygen cylinders or stable electricity.

The project integrates **hardware design, embedded systems, sensors, and communication modules** to ensure safe and reliable oxygen delivery.

---

## ⚙️ System Architecture

### Main Components
- Pressure Swing Adsorption (PSA) oxygen concentrator  
- Zeolite 13X molecular sieve  
- Arduino UNO controller  
- OOM202 medical-grade oxygen sensor  
- ADS1115 16-bit ADC  
- GSM module (SIM600A)  
- GPS module (NEO-6M)  
- OLED display  
- MAX30100 (SpO₂ & heart rate sensor)  

---

## 🔄 Pressure Swing Adsorption (PSA) Cycle

### Process Summary
- Compressed air enters **zeolite canister Z1** → nitrogen adsorption  
- Oxygen is collected in a **storage tank**  
- Nitrogen is purged using oxygen from **Z2**  
- Cyclic operation ensures **continuous oxygen output**  

**Oxygen concentration achieved:** 30% – 80%  
**Flow rate:** Suitable for single-patient use  

---

## 🧪 Oxygen Analyzer & Calibration
- Medical-grade **OOM202 oxygen sensor**  
- Output range: **0–76 mV for 0–100% O₂**  
- High-resolution **ADS1115 (16-bit ADC)** used for accurate measurement  

### Calibration Performed Using
- Ambient air (20.95% O₂)  
- 99.7% pure oxygen  
- Helium gas (0% O₂)  

---

## 🚨 Fault Detection & Alert System

### Continuous Monitoring
- Oxygen purity  
- SpO₂  
- Heart rate  

### Alert Mechanism
- Automatic **SMS alerts via GSM**
- **GPS coordinates** sent to service provider in case of:
  - Low oxygen purity  
  - Sensor failure  
  - System fault  

---

## 💻 Software Implementation
**Platform:** Arduino  

### Key Features
- Sensor data acquisition using ADS1115  
- Oxygen percentage calculation  
- OLED display output  
- GSM SMS alert using AT commands  
- GPS-based location reporting  

📂 **Code available in `/software`**

---

## 🧠 Key Engineering Skills Demonstrated
- Embedded systems (Arduino, I2C, ADC)  
- Sensor interfacing & calibration  
- Medical device instrumentation  
- PSA-based gas separation  
- Hardware–software integration  
- Fault detection & alert systems  
- GSM/GPS communication  

---

## 📄 Documentation
📘 **Full Technical Report:**  
[Oxygen Concentrator Report](docs/Oxygen Concentrator Report.pdf)

---

## 🔮 Future Improvements
- Closed-loop oxygen purity control  
- Battery optimization for portability  
- Mobile app for remote monitoring  
- Custom PCB design  
