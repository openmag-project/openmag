<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# Overview

## Goal

The goal of this REDMAG guide is to document—clearly and thoroughly—how REDMAG media behaves from the perspective of:

1. **SSD internals** (controller, NAND, firmware, DRAM, power behavior)  
2. **RED camera validation** (what the camera checks, and why mismatches fail)  
3. **Tooling and workflow** (how researchers identify components, choose tools, and validate results)  
4. **Repeatable research reporting** (how to capture evidence and share findings responsibly)

This is intended to be a practical, engineering-focused guide you can follow end-to-end.

---

## Problem Statement (rolled into the overview)

DSMC1-era RED cameras using **REDMAG** media rely on firmware-level validation to determine whether attached SSD media is “recognized” and allowed for recording. These checks prevent many generic SATA SSDs from being accepted, even when the underlying hardware can sustain recording bandwidth.

As official REDMAG media becomes increasingly scarce, expensive, or discontinued, users maintaining legacy systems need a structured way to:

- understand the requirements,
- test candidates safely,
- document results accurately.

---

## What REDMAG validation checks (observed)

Through firmware analysis and hands-on testing, REDMAG acceptance is observed to depend primarily on **two values**:

- **SSD Model Number** (ATA Identify “Model” string) (example: RED 512GB V4)
- **Reported Capacity** (logical addressable capacity exposed by the SSD) (example: 512GB)

The camera firmware extracts capacity encoded in the model string (e.g., “256GB”) and compares it to the drive’s reported capacity. These must match exactly. That's it! Nothing more!

Key observations:

- REDMAG does **not** validate `0x90h` / `0x91h` S.M.A.R.T. Host Vendor logs (those are MINIMAG-related).
- Camera-side **power is not required** for basic SATA identity detection (data only can be sufficient), though most real setups use camera power.
- Exact **spacing and capitalization** of model strings matters.

---

## Guide map

- **SSD Guide**: deep SSD anatomy + what makes a “cinema-friendly” SSD  
- **Hardware Guide**: adapters, cables, power, and bench setup that prevents false failures  
- **REDMAG Validations Overview**: the camera’s decision logic (whitelist + capacity)  
- **MP Tool Guide**: how researchers identify controller/NAND, select tools, configure, and flash  
- **Working Example**: a documented test case with screenshot placeholders
---

⬅️ Prev: [Contents](README.md)  
➡️ Next: [SSD Guide](02-ssd-guide.md)
