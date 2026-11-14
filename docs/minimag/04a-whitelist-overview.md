<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# Whitelist Overview

## Model covered by the source

The supplied PDF documents one target model:

```text
RED 480GB V1
```

Use exactly one space between `RED` and `480GB`, and one before `V1`. The source does not provide a complete MINIMAG whitelist or verified settings for other capacities.

---

## Other identity fields

| MP tool field | Value | Entry guidance |
| --- | --- | --- |
| Vendor Specific | `Red Digital ` | Capital R and D, one internal space, **one trailing ASCII space**. |
| Begin Serial / End Serial | `P1T1400508641101XXXX` | Replace the final four Xs with digits; use the same value for both on a single drive. |
| SN Length | `20` | Preserve the complete 20-character serial. |
| Firmware Version | `0308-000` | Reported identity string; not a firmware package filename. |

For example, `P1T14005086411010001` follows the source's serial pattern. Choose a unique suffix for each research drive and retain its original hardware identity in your notes. The source explicitly leaves the serial and firmware fields' necessity unconfirmed.

---

## Make the trailing space visible

The vendor value contains **12 characters**, including its final space. This notation makes the boundary visible:

```text
|Red Digital |
```

The vertical bars are delimiters for this illustration; **do not enter them** in the MP tool. Type `Red Digital`, then press Space once. A Markdown table or screenshot may not visibly distinguish that final space.

Do not reuse REDMAG's `Rev T` or `512GB` strings for this workflow. Follow the [MP Tool Guide](05-mp-tool-guide.md) for where to enter these fields.

---

Prev: [MINIMAG Validations Overview](04-minimag-validations-overview.md)  
Next: [Capacity Overview](04b-capacity-overview.md)
