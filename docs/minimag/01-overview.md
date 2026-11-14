<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# Overview

## Goal

Document the supplied guide's workflow for configuring a compatible SATA SSD as a **RED 480GB V1** MINI-MAG profile, from hardware identification through camera testing.

This guide separates SSD requirements, bench setup, camera validation, and programming so that each stage can be checked before proceeding.

---

## Scope and compatibility

The source PDF reports successful use on **RED DSMC2 cameras running firmware v7.4.1**, described there as current as of March 2026. That is the source's dated compatibility claim, not a statement about today's latest firmware or independent verification by openMAG. Compatibility with other camera models, firmware versions, capacities, and controller families is not established here.

The worked profile is **480GB**. The PDF's subtitle says “any SATA drive,” but its procedure requires a supported controller, matching NAND tooling, physical DRAM, sufficient native capacity, and suitable sustained performance. Acceptance by a camera does not establish recording reliability.

---

## What the workflow changes

A Mass Production (MP) tool initializes the SSD's firmware, NAND configuration, and identity fields. The source uses Silicon Motion (SMI) tools to set the model, vendor-specific string, serial, and reported firmware version. Linux `hdparm` then sets the visible sector count through the Host Protected Area (HPA).

The source describes model identity and capacity as the main camera checks. It also prescribes other identity fields, while explicitly noting that the serial and firmware requirements have not been confirmed. Treat this as a reported working profile rather than a complete analysis of camera validation.

**Programming erases the drive and can permanently damage it.** Use an expendable test SSD and back up any data before proceeding. Read the repository's [disclaimer](../../legal/DISCLAIMER.md), [liability limitations](../../legal/LIABILITY.md), and [educational-use statement](../../legal/EDUCATIONAL_USE.md).

---

## Guide map

- **SSD Guide**: controller, NAND, DRAM, form factor, and sustained-write requirements.
- **Hardware Guide**: Windows host, adapters, power, Linux USB, and recovery connections.
- **MINIMAG Validations Overview**: the reported identity profile and exact capacity.
- **MP Tool Guide**: identify hardware, select a tool, configure, program, and verify.
- **Linux Sector Count Guide**: set and verify the persistent visible capacity.
- **Working Example**: follow the 480GB workflow and record your own results.
- **Troubleshooting & Recovery**: diagnose detection, programming, capacity, and recording failures.
- **Quick Reference**: parameters, commands, and source links.

---

## Source and editorial notes

Adapted from the supplied 16-page `minimag-guide.pdf`, titled **RED 480GB MINI-MAG® SPOOFING — How to Use Any SATA Drive With Your DSMC2**. The PDF was supplied locally; no public source URL or author is identified in this port. Its configuration figure is reproduced in the MP Tool chapter. Repeated page footers and broken PDF numbering have been replaced by the repository's chapter navigation.

The port retains the source's profile and workflow while distinguishing reported results from unverified requirements. It corrects the HPA example's enabled/disabled interpretation, adds explicit drive identification and post-power-cycle verification, and does not carry forward the source's generic sleep/cable-unplug “unfreeze” procedure as a universal remedy. A DRAM chip is retained as a requirement of this workflow, without presenting it as a guarantee of speed or the only cause of dropped frames.

RED, MINI-MAG, and DSMC2 are trademarks of their respective owners. This project is not affiliated with or endorsed by RED; see [trademark disclosures](../../legal/TRADEMARKS.md).

---

Prev: [Contents](README.md)  
Next: [SSD Guide](02-ssd-guide.md)
