FLEX_PART_HANDLER_2025

A compact FANUC robot handler program demonstrating integrated motion logic, CNC loading, and vision-based automation in a single file.

Overview

This project implements a self-contained FANUC handling routine designed for flexible part transfer between inbound vision pickup, CNC loading/unloading, and optional finishing. All subroutines are inlined for portability and testing.

Features

Inline tool logic (TOOL_LIGHT) — no external CALLs required.

Vision-guided pickup with configurable timeouts and offset generation.

CNC interface integration with retry logic and fault handling.

Optional finishing cycle (debur/polish) controlled by mode selection.

Adaptive drop-slot sequencing and regrip logic.

Safe abort path that de-energizes all outputs before returning home.

Parameter Summary
Register	Function	Default
R[20]	Vision timeout (s)	5.0
R[21]	Gripper timeout (s)	3.0
R[30]	Chuck timeout (s)	4.0
R[40]	Load retries	3
R[22]	Drop pitch (mm, +Y)	150
R[28]	Max drop slots	8
R[90]	Mode select (1 = Full, 2 = Skip Finish, 3 = Test Only)	—
Logic Flow
[START]
 → Vision Pickup  
 → CNC Load  
 → Finish (optional)  
 → CNC Unload  
 → Regrip  
 → Drop  
 → Summary / Loop

Repository Structure
FLEX_PART_HANDLER_2025_LIGHT_ONLY.LS   # Main program (inline tool logic)
README.md                              # Documentation and flow summary

Notes

Developed as a portfolio-safe FANUC automation model demonstrating motion sequencing, error handling, and integration patterns for industrial robotics.
