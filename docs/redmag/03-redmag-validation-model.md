<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# REDMAG Validation Model

REDMAG validation is significantly simpler than MINIMAG.

Through firmware analysis and testing, REDMAG validation has been observed to check:

1. SSD model name
2. SSD capacity

These checks explain why a drive may be detected and formatted but still record with limitations.

## Model name whitelist

The camera firmware contains a whitelist of approved REDMAG model names.
The SSD’s reported model string must match one of these entries **exactly**.

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

It is common to use the latest revision (for example, **RED 256GB Rev T3**
or **RED 512GB V4**), but **any whitelisted entry can work** as long as the
reported SSD capacity matches the capacity encoded in the model name **exactly**.

## Capacity verification

The camera extracts the capacity value embedded in the model name string
and compares it against the SSD’s reported capacity.

Any mismatch will trigger recording restrictions.

## What you should record before changing anything

Before you attempt any modifications or experiments, record the SSD’s current identity.
This is useful for troubleshooting and for community reports.

On Linux or macOS (with smartmontools installed), you can collect basic identify info:

- model string
- firmware version
- reported capacity
- SATA link speed (if available)

> Placeholder: example screenshots for `smartctl` output



---

[← REDMAG storage hardware](02-redmag-storage-hardware.md) | **REDMAG validation model** | [Recording restrictions →](04-recording-restrictions.md)
