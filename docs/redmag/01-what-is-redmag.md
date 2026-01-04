<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# What is REDMAG?

REDMAG is proprietary SSD-based recording media used with several RED camera generations.

At a hardware level, a REDMAG unit typically includes:

1. A standard **SATA SSD module** (most commonly **microSATA** or **mSATA**)
2. A **RED-designed PCB pass-through board**
3. An enclosure + connector that mates with the camera

From the camera’s perspective, REDMAG appears as a **SATA storage device**.

## Key implication

Because the camera speaks **SATA**, any replacement approach must ultimately present a valid SATA device to the camera.

- SATA SSDs: compatible at the protocol level
- NVMe (PCIe): not compatible
- USB “bridge” solutions: not compatible unless they present as a true SATA device to the camera (most do not)

## Why REDMAG replacement is challenging

The challenge is not “is it SATA?”—the challenge is that the camera performs **media validation** based on:
- the SSD’s reported **model name string**
- the SSD’s reported **capacity**
- a whitelist embedded in camera firmware

If any of those checks fail, the camera may still detect the media but restrict recording.



---

[← REDMAG Index](README.md) | **What is REDMAG?** | [Storage hardware deep dive →](02-redmag-storage-hardware.md)
