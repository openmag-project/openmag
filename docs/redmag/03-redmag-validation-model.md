<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# REDMAG Validation Model and Whitelist

REDMAG validation (as observed through firmware analysis and testing) checks two things:

1. SSD **model name string**
2. SSD **reported capacity**

If either fails, the camera may still detect/format the media but will restrict recording.

## Capacity limit

**512GB is the maximum supported REDMAG capacity** based on the known whitelist entries.

## Model name whitelist

The SSD’s reported model string must match one of these values **exactly** (including spacing and punctuation).

### 64GB models
- RED 64GB Rev A1
- RED 64GB Rev T1
- RED 64GB Rev T2
- RED 64GB Rev T3

### 128GB models
- RED 128GB Rev T1
- RED 128GB Rev T2
- RED 128GB Rev T3

### 256GB models
- RED 256GB Rev T1
- RED 256GB Rev T2
- RED 256GB Rev T3

### 512GB models (maximum)
- RED 512GB V1
- RED 512GB V2
- RED 512GB V3
- RED 512GB V4

It is common to use the latest revision (for example **RED 256GB Rev T3** or **RED 512GB V4**),
but any whitelisted entry can work if the capacity check passes.

## The capacity check (why “close enough” fails)

The camera extracts the capacity number from the model string (for example “256GB”)
and compares it to the SSD’s reported capacity.

These must match **exactly**. “Almost the same size” will fail.

This is also why some “256GB-class” SSDs fail: manufacturers may ship drives that report slightly different
usable capacities depending on over-provisioning and firmware.

## What to document before you change anything

Before experimenting, collect and store a baseline identity record for the SSD.

Minimum fields:
- Model (as reported by the SSD)
- Firmware version
- Reported capacity (in bytes, if possible)
- Controller identification (if known)
- NAND identification (if known)

### Suggested read-only tools (identity collection)

- `smartctl` (smartmontools) on Linux/macOS/Windows
- `hdparm -I` (Linux) for SATA identify summary
- Vendor “SSD Toolbox” utilities (read-only usage where possible)

> Placeholder: paste example command outputs and screenshots for each platform.



---

[← Storage hardware deep dive](02-redmag-storage-hardware.md) | **Validation model and whitelist** | [Recording restrictions →](04-recording-restrictions.md)
