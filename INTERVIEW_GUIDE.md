# Interview Presentation & Deep Technical Q&A Guide: Sequence Quest

## 🎤 How to Present This Project (Elevator Pitch)
"**Sequence Quest** is a real-time embedded C application running on an Infineon/Cypress PSoC microcontroller. My partner Varun and I developed it to read numeric input sequences from a 4x4 matrix keypad, validate mathematical sequence rules in real time, and output converted Binary Coded Decimal (BCD) values over UART."

---

## 💡 Key Architectural & Technical Highlights
- **Non-blocking Debouncing**: Timer-interrupt driven keypad polling to avoid CPU delay stalls.
- **Efficient BCD Conversion**: Implements the Shift-Add-3 (Double Dabble) algorithm for fast hex-to-BCD conversion.
- **Bitwise State Processing**: Optimized bitwise operations for real-time sequence validation.

---

## ❓ Deep Technical Interview Questions & Prepared Humble Answers

### Q1: "How did you implement non-blocking keypad debouncing?"
> **Humble Answer**: *"Rather than using simple delay loops which waste CPU bandwidth, we set up a hardware timer ISR that fires every 10ms. The ISR scans matrix rows and columns and requires a pin reading to stay stable across three consecutive samples before confirming a key press. This kept the core CPU free for UART communication and bitwise sequence parsing."*

### Q2: "In bare-metal Embedded C on PSoC, how did you access hardware registers for the keypad matrix?"
> **Humble Answer**: *"We used Infineon Peripheral Driver Library (PDL) APIs like `Cy_GPIO_Read()` for high-level pin reading. However, during debugging, we inspected the physical register base addresses (like `GPIO_PRT_IN`) in the PSoC Technical Reference Manual to understand bit masking and register offsets. Using driver APIs gave us clean, portable code, while understanding register bit manipulation helped us debug low-level GPIO state transitions."*

### Q3: "How did you prevent race conditions between the main loop processing sequences and the timer ISR?"
> **Humble Answer**: *"We declared shared variables as `volatile` (e.g., `volatile bool g_keyPressed`) to prevent compiler optimizations from caching outdated register values. Additionally, we kept the ISR execution window minimal—capturing only raw key scan codes—and deferred heavy sequence validation logic to the main loop to keep interrupt latency low."*

### Q4: "Why did you use Binary Coded Decimal (BCD) conversion and how does Shift-Add-3 work?"
> **Humble Answer**: *"In embedded systems driving 7-segment displays or numeric outputs, BCD makes individual decimal digit extraction trivial without requiring expensive runtime division operations. Implementing the Shift-Add-3 algorithm allowed us to convert values efficiently in hardware-friendly bit shifts."*

### Q5: "What embedded debugging tools did you use during development?"
> **Humble Answer**: *"We used a combination of UART terminal logging, logic analyzers to verify matrix row/column timing during key presses, and PSoC Creator's built-in debugger to inspect register states."*
