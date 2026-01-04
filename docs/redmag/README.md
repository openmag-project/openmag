<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# REDMAG Documentation

This section is a practical, beginner-friendly guide to understanding and validating **REDMAG** media, with enough technical depth
for engineers to reproduce results and contribute evidence.

This guide is REDMAG-only. MINIMAG is documented separately.

## What you will learn and do

- Understand how REDMAG media is built (internal SATA SSD + pass-through PCB)
- Understand exactly what the camera validates for REDMAG (model name whitelist + capacity match)
- Build a safe test bench and repeatable validation routine (detect → format → record → offload → verify)
- Select SSDs that are more likely to behave well under sustained cinema writes (NAND + DRAM + power behavior)
- Document results in a way the community can reproduce

## Known capacity limit

**512GB is the maximum supported REDMAG capacity** based on the known whitelist. Drives larger than 512GB are not expected to pass validation.

## Reading order

1. [What is REDMAG?](01-what-is-redmag.md)
2. [Storage hardware deep dive](02-redmag-storage-hardware.md)
3. [REDMAG validation model and whitelist](03-redmag-validation-model.md)
4. [Recording restrictions and symptoms](04-recording-restrictions.md)
5. [End-to-end workflow (safe + repeatable)](05-high-level-process.md)
6. [MP Tools overview (general, vendor-agnostic)](06-mp-tools-overview.md)
7. [Adapters, power, and external testing](07-adapters-and-power.md)
8. [Known gotchas and troubleshooting](08-known-gotchas.md)



---

  | **REDMAG Index** | [What is REDMAG? →](01-what-is-redmag.md)
