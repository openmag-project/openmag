<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# Known Gotchas and Troubleshooting

This page focuses on isolating causes in a controlled way.

## Symptom: camera freezes when media is inserted
Most likely causes:
- adapter signal integrity
- power sag during enumeration
- short/ground issue in adapter wiring

Isolation steps:
- test SSD on a computer with the same adapter
- switch to external power (if applicable)
- reduce adapters/cable length

## Symptom: format fails or hangs
Common causes:
- unstable SATA link
- SSD firmware behavior under trim/format patterns
- power instability

Isolation steps:
- repeat format after a cold reboot
- try a different adapter/cable
- confirm SSD health via SMART on a computer

## Symptom: records short clips but fails under stress
Common causes:
- sustained write performance collapse (cache exhausted)
- thermal throttling
- DRAM-less SSD behavior

Isolation steps:
- run a sustained write benchmark on a computer
- monitor temperature if possible
- prefer DRAM-based SSDs / better NAND

## Symptom: offloaded clips corrupted
Common causes:
- intermittent disconnects during record
- power drop under write burst
- adapter instability

Isolation steps:
- check connectors and strain relief
- repeat offload with checksum verification
- do not trust “it played once” as proof of integrity

## Golden rule

Change one variable at a time and document results.



---

[← Adapters and power](07-adapters-and-power.md) | **Gotchas and troubleshooting** |
