<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# MINIMAG Validations Overview

## What validation means

Recognition, permission to format, and reliable recording are separate outcomes. Check and document all three.

The PDF describes a working **RED 480GB V1** identity and sector-count profile on DSMC2 firmware v7.4.1. It does not supply firmware-analysis evidence establishing every validation check, and it does not establish support for arbitrary SATA drives.

---

## Reported inputs

| Field | Profile in the source | Evidence limit |
| --- | --- | --- |
| Model | `RED 480GB V1` | Source identifies this as a whitelist match. |
| Vendor Specific | `Red Digital ` | Source requires one trailing space. |
| Serial | `P1T1400508641101XXXX` | Source recommends unique final digits; necessity is unconfirmed. |
| Reported firmware | `0308-000` | Source uses this value; necessity is unconfirmed. |
| Visible sector count | `937703088` | Source specifies an exact match for this profile. |

Changing the reported firmware string does not mean the drive runs original RED firmware. The MP tool programs its controller/NAND-specific firmware package.

The REDMAG overview mentions MINIMAG host-vendor logs `0x90` / `0x91`; the supplied PDF does not document those logs or a procedure for them. This port does not infer additional checks or log modifications from that mention.

---

## What to record

- Camera model and firmware version.
- SSD retail model, PCB revision, controller, NAND, and DRAM.
- Exact identity fields, preserving case and spaces.
- Visible/native sector counts, logical sector size, and adapter.
- MP tool version and saved configuration.
- Camera warnings verbatim, format result, recording settings, clip duration, and read-back outcome.

Do not infer reliability from recognition alone, or broader compatibility from a single test.

---

## This section's subpages

- [Whitelist Overview](04a-whitelist-overview.md): the single profile covered by the PDF.
- [Capacity Overview](04b-capacity-overview.md): sector arithmetic and the distinction from REDMAG configuration.

---

Prev: [Hardware Guide](03-hardware-guide.md)  
Next: [Whitelist Overview](04a-whitelist-overview.md)
