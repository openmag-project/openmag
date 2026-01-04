<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# REDMAG Validation Model

REDMAG validation is significantly simpler than MINIMAG.

Through firmware analysis and testing, REDMAG validation has been observed to check:

1. SSD model name
2. SSD capacity

## Model name whitelist

The camera firmware contains a whitelist of approved REDMAG model names.
The SSD’s reported model string must match one of these entries **exactly**.

This project will document the known whitelist values.

## Capacity verification

The camera extracts the capacity value embedded in the model name string
and compares it against the SSD’s reported capacity.

These values **must match exactly** or recording will be restricted.

> Placeholder: whitelist table

---
**Navigation**
- **Previous:** [REDMAG storage hardware](02-redmag-storage-hardware.md)
- **Up:** [REDMAG Index](README.md)
- **Next:** [Recording restrictions](04-recording-restrictions.md)
