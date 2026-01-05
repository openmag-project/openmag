<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# Capacity Overview

## What “capacity” means to a camera

At the device level, capacity is usually expressed as:
- total logical sectors (LBAs),
- logical sector size (commonly 512 bytes),
- total user addressable bytes = LBAs × sector size.

Many tools also show:
- “user capacity” in bytes,
- nominal marketing size (GB),
- binary size (GiB).

For REDMAG, the camera expects the **capacity embedded in the model string** to match the device’s **reported capacity**.

---

## Why exact matches matter

Observed behavior indicates that the firmware:
- extracts the numeric capacity token (e.g., 256GB),
- compares it to the SSD’s reported capacity,
- requires exact matching.

This is why:
- a correct model string with incorrect reported capacity fails,
- a correct capacity with an unrecognized model string fails.

---

## Common mismatch causes

- Using the wrong capacity selector in an MP tool (e.g., not selecting IDEMA)
- Bridge adapters that misreport sector counts
- Firmware-level overprovisioning being exposed incorrectly
- Decimal vs binary confusion when humans eyeball results (the camera uses the real numbers)

---

## What to record in your notes

Capture:
- total LBAs/sectors from Identify Device,
- logical sector size,
- reported bytes from at least one tool,
- camera behavior (format/record).

A good habit is to paste tool output into your notes so spacing and numbers are preserved.
---

⬅️ Prev: [Whitelist Overview](whitelist-overview.md)  
➡️ Next: [MP Tool Guide](mp-tool-guide.md)

