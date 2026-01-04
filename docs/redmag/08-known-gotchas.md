<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# Known Gotchas

This page collects the most common failure modes and “surprises” encountered by the community.

## Hardware variability

- SSD manufacturers may change controllers without notice
- NAND revisions can break tooling compatibility
- identical-looking SSDs can behave differently under sustained write

## Adapter instability

- SATA adapters often introduce instability (especially SATA-to-microSATA)
- camera freezes during detect or format are often adapter-related
- intermittent disconnects can corrupt footage

## Validation mismatches

- capacity mismatches trigger recording limits
- whitespace or punctuation differences in model name strings can fail validation

## Practical safety rules

- make one change at a time
- validate with the same sequence every time
- keep a baseline device unchanged
- prefer stable power and minimal adapters

This list will grow as the community contributes findings.



---

[← Adapters and power](07-adapters-and-power.md) | **Known gotchas** |
