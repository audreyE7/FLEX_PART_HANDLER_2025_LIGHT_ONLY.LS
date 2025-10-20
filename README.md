# 🤖 FLEX_PART_HANDLER_2025_LIGHT_ONLY

**Author:** Audrey Enriquez  
**Controller:** FANUC R-30iB+  
**Language:** TP / LS  
**Revision:** v2025.10.19  
**Tooling:** LIGHT (0.5 kg payload gripper)

---

## 🧩 Overview

`FLEX_PART_HANDLER_2025_LIGHT_ONLY` is a **self-contained robot handler** for CNC automation cells.  
It performs **vision-guided pickup**, **CNC load/unload**, **finishing**, **regrip**, and **drop-off** without any external subprograms.  
All tool and payload logic are **inlined**, enabling fast testing and simplified integration for new operators.

---

## ⚙️ Features

- ✅ Inline tool setup (`TOOL_LIGHT`) — no external macros  
- 🔍 Vision pickup with offset correction and timeout recovery  
- 🏗️ CNC interface control (open/close chuck, position retries)  
- ✨ Optional finishing cycle with spindle control  
- 📦 Sequential drop-off slot tracking  
- 🧠 Configurable parameters for timeouts, retries, and pitch spacing  
- 🛑 Safe ABORT sequence (returns home, drops all outputs)  

---

## 🧮 Parameter Summary

| Register | Function | Default |
|-----------|-----------|----------|
| `R[20]` | Vision timeout (s) | 5.0 |
| `R[21]` | Gripper timeout (s) | 2.0 |
| `R[30]` | Chuck timeout (s) | 4.0 |
| `R[31]` | Max load retries | 3 |
| `R[22]` | Drop pitch (mm, +Y) | 150 |
| `R[32]` | Max drop slots | 8 |
| `R[90]` | Mode Select — `1=Full`, `2=SkipFinish`, `3=TestOnly` | — |

---

## 🧠 Program Flow

```text
[START]
   ↓
[VISION PICKUP]
   ↓
[CNC LOAD]
   ↓
[FINISH] (skipped if mode=2)
   ↓
[CNC UNLOAD]
   ↓
[REGRIP]
   ↓
[DROPOFF]
   ↓
[SUMMARY → LOOP]
```

---

## 🧰 I/O Mapping (Example)

| Digital Input (DI) | Description |
|---------------------|-------------|
| 10 | Gripper closed sensor |
| 11 | Gripper open sensor |
| 108 | CNC chuck open confirm |
| 109 | CNC chuck closed confirm |
| 110 | CNC ready signal |
| 121 | Regrip station open sense |

| Digital Output (DO) | Description |
|----------------------|-------------|
| 10 | Gripper close command |
| 11 | Gripper open command |
| 105 | CNC chuck open |
| 106 | CNC chuck close |
| 110 | Finishing tool spindle |
| 120 | Regrip open |
| 100 | Status flag (end/heartbeat) |

---

## 🚦 Mode Logic

| Mode | Behavior |
|------|-----------|
| `1 – Full Cycle` | Executes pickup → CNC → finish → unload → regrip → drop |
| `2 – SkipFinish` | Bypasses finishing spindle sequence |
| `3 – TestOnly` | Performs vision pickup and immediate drop-off (no CNC) |

---

## 💡 Future Improvements

- Add `HEAVY_TOOL` variant with 5 kg payload calibration  
- Integrate live vision feedback via `$MNUTOOL` offset update  
- Log error counts & timeouts for diagnostics  
- Optional torque/force verification for gripper engagement  

---

## 📁 Repository Structure

```
├── FLEX_PART_HANDLER_2025_LIGHT_ONLY.LS   ← main program
├── FLEX_PART_HANDLER_2025_HEAVY_TOOL.LS   ← (future variant)
├── /docs/
│   ├── IO_MAP.md
│   ├── FLOW_DIAGRAM.png
│   └── PAYLOAD_TABLE.csv
└── README.md   ← this file
```

---

## 🧾 License & Usage

This project is for **educational and demonstration** purposes only.  
You are free to reuse or adapt the logic for academic, research, or industrial training under proper safety conditions.

---

### 🪄 Author Note
This handler was originally derived from a FANUC cell integration at **Permaswage / PCC**  
and simplified for demonstration in simulation and GitHub portfolio use.
