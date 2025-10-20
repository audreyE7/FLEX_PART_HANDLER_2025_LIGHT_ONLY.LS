# 🧰 IO_MAP.md — FLEX_PART_HANDLER_2025_LIGHT_ONLY

## 🧩 Digital Inputs (DI)

| Input # | Label | Description |
|----------|--------|-------------|
| DI[10] | GRIPPER_CLOSED | Confirms gripper jaws closed |
| DI[11] | GRIPPER_OPEN | Confirms gripper jaws open |
| DI[108] | CHUCK_OPEN_CONF | CNC chuck open confirmation |
| DI[109] | CHUCK_CLOSED_CONF | CNC chuck closed confirmation |
| DI[110] | CNC_READY | CNC ready for load/unload |
| DI[121] | REGRIP_OPEN_SENSE | Regrip station open detected |
| DI[21] | VISION_FOUND | Vision AI confirmed part location |

---

## 🔧 Digital Outputs (DO)

| Output # | Label | Description |
|-----------|--------|-------------|
| DO[10] | GRIPPER_CLOSE_CMD | Closes the gripper |
| DO[11] | GRIPPER_OPEN_CMD | Opens the gripper |
| DO[105] | CNC_CHUCK_OPEN | Opens CNC chuck |
| DO[106] | CNC_CHUCK_CLOSE | Closes CNC chuck |
| DO[110] | TOOL_SPIN | Activates finishing spindle |
| DO[120] | REGRIP_OPEN | Opens regrip fixture |
| DO[100] | STATUS_END | Signals program end / heartbeat |

---

## ⚙️ Registers (R)

| Register | Name | Description | Default |
|-----------|------|-------------|----------|
| R[20] | VISION_TMO | Vision timeout (s) | 5.0 |
| R[21] | GRIP_TMO | Gripper timeout (s) | 2.0 |
| R[30] | CHUCK_TMO | Chuck timeout (s) | 4.0 |
| R[31] | LOAD_RETRY_MAX | Max load retries | 3 |
| R[22] | DROP_PITCH | Drop spacing (+Y, mm) | 150 |
| R[32] | MAX_SLOTS | Max number of drop slots | 8 |
| R[90] | MODE_SELECT | Operation mode: 1=Full, 2=SkipFinish, 3=TestOnly | — |
| R[1] | PART_COUNT | Current cycle count | 0 |

---

## 🧭 Frames & Tools

| Type | Index | Name | Purpose |
|-------|--------|------|----------|
| UTOOL[1] | TOOL_LIGHT | Light gripper TCP |
| UTOOL[2] | TOOL_LOAD | CNC loading position |
| UTOOL[3] | TOOL_FINISH | Finishing tool spindle |
| UTOOL[4] | TOOL_REGRIP | Regrip handoff TCP |
| UFRAME[2] | VISION_FRAME | Camera reference frame |
| UFRAME[3] | CNC_FRAME | CNC coordinate system |
| UFRAME[4] | DROP_FRAME | Part drop area |
| UFRAME[5] | FINISH_FRAME | Finishing area frame |
| UFRAME[6] | REGRIP_FRAME | Regrip station frame |

---

## 🧠 Safety & Interlocks

- All major actuations (gripper, chuck, spindle) include DI confirmation checks.  
- Each motion sequence contains timeout handling and retry logic.  
- Abort sequence drops all outputs and returns robot to **SAFE HOME**.  
- Vision and CNC subsystems operate independently under timeout supervision.
