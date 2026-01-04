<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# MP Tools Overview

MP (Manufacturing Process) Tools are low-level utilities used by SSD vendors to configure,
test, and provision drives during manufacturing.

They can expose settings that normal consumer utilities do not, including device identity,
capacity configuration, and controller-specific parameters.

## Why MP Tools are hard to use

MP Tools are rarely “one tool fits all.” They often depend on:
- SSD controller family and revision
- NAND type and revision
- sometimes even PCB layout variants

Even within the same retail SSD model, manufacturers may silently change controller/NAND
over time, which can break compatibility with previously working tools.

## Risks and realities

MP Tools are high risk:
- incorrect settings can permanently brick an SSD
- configuration may be non-reversible without specialized equipment
- mistakes can lead to unstable media and corrupted footage

## How openMAG helps

This project aims to maintain a community-maintained matrix of:
- SSD model and hardware revision
- controller identification
- NAND identification
- tested tooling and outcomes (when contributors provide evidence)

This information helps reduce trial-and-error, but does not eliminate risk.

> Placeholder: MP Tool screenshots (redacted where appropriate)



---

[← High-level process](05-high-level-process.md) | **MP Tools overview** | [Adapters and power →](07-adapters-and-power.md)
