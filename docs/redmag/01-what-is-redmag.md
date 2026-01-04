<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# What is REDMAG?

REDMAG is RED Digital Cinema’s proprietary SSD-based recording media used in
RED ONE, EPIC, and SCARLET cameras.

At a hardware level, REDMAG units are typically composed of:

1. A standard SATA SSD module (most commonly **microSATA** or **mSATA**)
2. A RED-designed PCB pass-through board
3. A physical enclosure and connector that mates with the camera

The RED PCB adapts the internal SSD module and presents a SATA device to the camera.
From the camera’s point of view, it is communicating with a SATA SSD.

## Why this matters

Because the underlying interface is SATA, successful REDMAG replacements require:
- a SATA device (not NVMe)
- stable power and signal integrity
- device identity and capacity values that pass the camera’s validation checks

## Form factors observed

Over the years, REDMAG units have been observed using:
- **microSATA** SSD modules (older units; scarce today)
- **mSATA** SSD modules (more available and often easier to work with)

Both are still SATA devices.

## What will not work

- **NVMe** drives (M.2 NVMe) — different protocol
- USB storage presented through adapters — not a native SATA device to the camera
- “looks similar” connectors that do not provide real SATA signaling



---

[← REDMAG Index](README.md) | **What is REDMAG?** | [REDMAG storage hardware →](02-redmag-storage-hardware.md)
