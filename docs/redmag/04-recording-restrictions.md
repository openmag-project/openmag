<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# Recording Restrictions and Symptoms

When validation fails, behavior commonly falls into one of these categories:

- **Media not detected**
- **Detected but unstable** (freezes, disconnects, format failures)
- **Detected and usable, but recording is restricted**

## Common restriction symptoms

Depending on camera model/firmware, you may see:
- unexpectedly short maximum record times
- warnings about media compatibility
- recording stops earlier than expected
- inconsistent behavior between reboots

## What typically causes restrictions (REDMAG)

Observed causes include:
- model string not on whitelist
- capacity mismatch between model string and reported capacity
- unstable SATA link (often adapters/cables)
- power instability (especially with externally powered setups)

This guide’s workflow focuses on isolating these causes one at a time.



---

[← Validation model and whitelist](03-redmag-validation-model.md) | **Recording restrictions** | [End-to-end workflow →](05-high-level-process.md)
