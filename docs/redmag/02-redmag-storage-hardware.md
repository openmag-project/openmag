<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# REDMAG Storage Hardware

REDMAG media consists of three primary components:

1. The SSD itself (microSATA or mSATA)
2. A RED-designed PCB pass-through adapter
3. The camera’s SATA interface

## microSATA

microSATA SSDs were used in early REDMAG units but are no longer commonly manufactured.
Modern replacements often require adapters.

**Common downside:** many SATA-to-microSATA adapters introduce instability
(signal integrity, pin mapping differences, power behavior). Instability often appears as:
- camera freezes during media detect or format
- intermittent disconnects
- random record stops or corrupt clips

## mSATA

mSATA SSDs are typically easier to work with:
- widely available
- no fragile SATA adapters required (in many builds)
- broader ecosystem support for identification and testing

For these reasons, **mSATA is currently the recommended approach**.

## Practical recommendation

If you are new to this work:
- start with mSATA
- keep one known-good REDMAG as your baseline
- document everything (photos, logs, exact part numbers)

> Placeholder: hardware photos, PCB diagrams, and example part numbers



---

[← What is REDMAG?](01-what-is-redmag.md) | **REDMAG storage hardware** | [REDMAG validation model →](03-redmag-validation-model.md)
