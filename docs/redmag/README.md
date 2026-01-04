<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# REDMAG Documentation

This section is a practical, beginner-friendly guide to understanding and validating **REDMAG** media.

It includes:
- what REDMAG is and how it’s built internally
- what the camera checks (validation model)
- how to safely test and confirm your SSD behaves correctly
- common pitfalls and recovery strategies

MINIMAG is excluded from this path and documented separately.

## What you will accomplish

By the end of this REDMAG guide, you should be able to:

- choose a practical SSD form factor for REDMAG experimentation
- read and record your SSD identity and capacity information
- understand what the camera is validating and why mismatches fail
- run safe validation tests (format, record, offload, checksum compare)
- troubleshoot the most common failure modes

## Important limits

- **512GB is the maximum supported REDMAG capacity** in the known whitelist.
  Larger capacities are not expected to pass the model/capacity checks.

## Reading order

1. [What is REDMAG?](01-what-is-redmag.md)
2. [REDMAG storage hardware](02-redmag-storage-hardware.md)
3. [REDMAG validation model](03-redmag-validation-model.md)
4. [Recording restrictions](04-recording-restrictions.md)
5. [High-level process](05-high-level-process.md)
6. [MP Tools overview](06-mp-tools-overview.md)
7. [Adapters and power](07-adapters-and-power.md)
8. [Known gotchas](08-known-gotchas.md)



---

  | **REDMAG Index** | [What is REDMAG? →](01-what-is-redmag.md)
