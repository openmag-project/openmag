<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# Adapters, Power, and External Testing

REDMAG validation requires a working SATA device presented to the camera.
In many setups, it is possible to supply external power while only passing
SATA data through the camera connection.

This can reduce risk and enable experimentation with alternate form factors.

## Why external power matters

External power can help you:
- test SSD behavior without relying on camera power delivery
- stabilize adapters that behave poorly under voltage drop
- prototype alternative enclosures or cabling

## Safe external testing workflow

1. Power the SSD externally using a stable SATA power source.
2. Connect SATA data to a host machine first and verify the drive enumerates reliably.
3. Only then connect SATA data to the camera path for detect/format/record testing.
4. If instability appears, stop and revert to your baseline setup.

## Supported protocols

- SATA: supported
- NVMe: not supported

Any custom adapter must still present a valid SATA device.

> Placeholder: wiring diagram and example adapter photos



---

[← MP Tools overview](06-mp-tools-overview.md) | **Adapters and power** | [Known gotchas →](08-known-gotchas.md)
