# PIC32CM5164LS00048 — Zephyr RTOS Documentation & Porting Guide

This repository contains the interactive documentation and architectural reference for porting and running **Zephyr RTOS** on the **Microchip PIC32CM5164LS00048** microcontroller and **PIC32CM LS00 Curiosity Nano** (`pic32cm_ls00_cnano`, EV41C56A).

---

## 🌐 Live Interactive Documentation

👉 **[Launch Interactive Documentation](https://sujandurai.github.io/zephy_hml/)** *(When GitHub Pages is enabled)*  
Or open [`index.html`](index.html) directly in any browser.

---

## 📑 Documentation Structure (4-Tab Suite)

1. **📖 Tab 1: Our History**
   - Chronological contributor journey from Air Quality Monitoring System to Zephyr RTOS exploration, identifying the missing SoC gap, opening GitHub Issue [#116364](https://github.com/zephyrproject-rtos/zephyr/issues/116364), collaborating with Microchip engineers (@NhMchp & @sunil-abraham), and aligning with RFC [#92168](https://github.com/zephyrproject-rtos/zephyr/issues/92168).

2. **⚖️ Tab 2: GC00 vs LS00 Technical Comparison**
   - Comprehensive 10-part technical comparison between the existing upstream reference (`pic32cm_gc00`) and the target (`pic32cm5164ls00048`):
     - **Part 1:** Hardware Specification Matrix
     - **Part 2:** Exact Memory Map & APB Peripheral Base Addresses
     - **Part 3:** NVIC IRQ Interrupt Numbers
     - **Part 4:** Directory Structure Comparison
     - **Part 5:** Kconfig Line-by-Line Changes
     - **Part 6:** DeviceTree (`.dtsi`) Changes
     - **Part 7:** Board DTS Comparison
     - **Part 8:** Driver Reuse Strategy
     - **Part 9:** Clock Tree Comparison (DPLL 72 MHz vs FDPLL96M 48 MHz)
     - **Part 10:** File Action Summary Matrix (Copy vs Modify vs New)
   - 📄 **[Download Full PDF Guide: GC00_vs_LS00_Complete_Comparison.pdf](GC00_vs_LS00_Complete_Comparison.pdf)**

3. **🏛️ Tab 3: SoC Architecture Guide (8-Point Breakdown)**
   - **1. SoC Overview & Purpose:** Silicon-level definition (Arm Cortex-M23, ARMv8-M).
   - **2. Folder Structure:** Exact `soc/microchip/pic32c/pic32cm_ls/` layout.
   - **3. Memory Mapping:** Flash (512 KB: `0x00000000` - `0x00080000`) & SRAM (64 KB: `0x20000000` - `0x20010000`).
   - **4. Clock Initialization:** OSC16M &rarr; GCLK1 (/16) &rarr; 1.0 MHz &rarr; FDPLL96M (LDR=47) &rarr; 48 MHz &rarr; GCLK0 &rarr; CPU.
   - **5. `soc_reset_hook()`:** Thumb assembly SRAM zero-init loop for ECC safety prior to clock switch.
   - **6. Peripheral Mapping:** APB bridge base addresses (NVMCTRL, MCLK, GCLK, OSCCTRL, PORTA, PORTB) defined via DeviceTree.
   - **7. ARM TrustZone-M:** Security attribution (Secure vs Non-Secure) and bus diagnostic guidance.
   - **8. 60-Second Meeting Summary:** Ready-to-speak project pitch.

4. **⚙️ Tab 4: Board Documentation & Programming Guide**
   - Board hardware specifications, clock & I/O features, pinout table, and flashing/debugging guides with **PyOCD**, **EDBG**, **GDB Server**, and **VSCode** `launch.json`.

---

## 🚀 Quick Build & Flash Commands

```bash
# Build Blinky sample for PIC32CM LS00 Curiosity Nano
west build -b pic32cm_ls00_cnano -p -s samples/basic/blinky

# Flash via west (PyOCD runner)
west flash

# Or flash directly with Alex Taradov EDBG CLI tool
edbg -b -t pic32cm5164ls00048 -pv -f build/zephyr/zephyr.bin

# Debug session with GDB
west debug
```

---

## 🔗 Key References

- **Zephyr Project GitHub Issue #116364:** [zephyrproject-rtos/zephyr#116364](https://github.com/zephyrproject-rtos/zephyr/issues/116364)
- **Zephyr Microchip Architecture RFC #92168:** [zephyrproject-rtos/zephyr#92168](https://github.com/zephyrproject-rtos/zephyr/issues/92168)
- **Microchip PIC32CM LS00 Product Page:** [PIC32CM5164LS00048](https://www.microchip.com/en-us/product/pic32cm5164ls00048)
- **Curiosity Nano Kit (EV41C56A):** [Microchip EV41C56A](https://www.microchip.com/en-us/development-tool/EV41C56A)

---

*Maintained by Sujan D (@sujandurai)*
