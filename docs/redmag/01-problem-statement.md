# openMAG REDMAG Guide

**Educational & Research Documentation**

> ⚠️ **Disclaimer**  
> This guide is provided strictly for educational and research purposes.  
> Modifying SSD firmware using manufacturer production (MP) tools is inherently risky and can permanently damage hardware.  
> You assume all responsibility for any data loss, device failure, or equipment damage.  
>  
> This project is not affiliated with or endorsed by RED Digital Cinema.


---

## Problem Statement

RED cinema cameras that used the REDMAG rely on proprietary SSD media that enforce strict device authentication and identification checks at the firmware level. These checks prevent the use of generic off-the-shelf SSDs, even when the underlying hardware is technically capable of meeting performance and reliability requirements.

As official RED media becomes increasingly scarce, expensive, or discontinued for DSMC1 cameras, users are left with limited options for maintaining and extending the usable lifespan of their equipment.

The camera firmware only check two things when using a REDMAG:
- SSD Model Number
- Reported capacity

The firmware extract the capacity in the model number and compares that to the reported capacity. These have to match exactly! The REDMAG does NOT check any other values including the 0x90h and 0x91h like the MINIMAG. You also do not need the cameras power, you can connect only the data SATA wire and it will work, but most people will want to use the cameras power.

This guide documents a research-based workflow for understanding these constraints and exploring how certain SSDs can be configured—at a low level—to present themselves in a way that is accepted by RED cameras.

This is **not an officially supported solution**, and success depends heavily on hardware selection, tooling availability, and careful execution.

---

⬅️ Prev: [Contents](README.md)  
➡️ Next: [Overview](02-overview.md)
