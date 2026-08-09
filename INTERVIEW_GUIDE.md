# Interview Presentation Guide: Sequence Quest

## 🎤 How to Present This Project (Elevator Pitch)
"**Sequence Quest** is a real-time embedded C application running on an Infineon/Cypress PSoC microcontroller. My partner Varun and I developed it to read numeric input sequences from a 4x4 matrix keypad, validate mathematical sequence rules in real time, and output converted Binary Coded Decimal (BCD) values over UART."

---

## 💡 Key Architectural & Technical Highlights
- **Non-blocking Debouncing**: Timer-interrupt driven keypad polling to avoid CPU delay stalls.
- **Efficient BCD Conversion**: Implements the Shift-Add-3 (Double Dabble) algorithm for fast hex-to-BCD conversion.
- **Bitwise State Processing**: Optimized bitwise operations for real-time sequence validation.

---

## ❓ Common Interview Questions & Prepared Humble Answers

### Q1: "How did you implement non-blocking keypad debouncing?"
> **Answer**: *"Rather than using simple delay loops which waste CPU bandwidth, we set up a hardware timer ISR that fires every 10ms. The ISR scans matrix rows and columns and requires a pin reading to stay stable across three consecutive samples before confirming a key press. This kept the core CPU free for UART communication and bitwise sequence parsing."*

### Q2: "Why did you use Binary Coded Decimal (BCD) conversion?"
> **Answer**: *"In embedded systems driving 7-segment displays or numeric outputs, BCD makes individual decimal digit extraction trivial without requiring expensive runtime division operations. Implementing the Shift-Add-3 algorithm allowed us to convert values efficiently in hardware-friendly bit shifts."*

### Q3: "What embedded debugging tools did you use during development?"
> **Answer**: *"We used a combination of UART terminal logging, logic analyzers to verify matrix row/column timing during key presses, and PSoC Creator's built-in debugger to inspect register states."*
