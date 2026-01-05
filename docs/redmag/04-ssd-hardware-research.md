# openMAG REDMAG Guide

**Educational & Research Documentation**

> ⚠️ **Disclaimer**  
> This guide is provided strictly for educational and research purposes.  
> Modifying SSD firmware using manufacturer production (MP) tools is inherently risky and can permanently damage hardware.  
> You assume all responsibility for any data loss, device failure, or equipment damage.  
>  
> This project is not affiliated with or endorsed by RED Digital Cinema.


---

## 1. SSD Hardware Research (Pre-Purchase)

Before purchasing any SSD, you **must** research the following:

- **Controller model**
- **NAND type and manufacturer**
- **Form factor**
  - mSATA  
  - microSATA  
  - M.2 SATA (not NVMe)  
  - 2.5" Sata  

### Why This Matters

MP Tools are **controller- and NAND-specific**.  
Purchasing an SSD without confirming these details often results in:

- No compatible MP Tool
- Inability to enter production mode
- Permanent device failure

> **Recommendation:**  
> Prioritize SSDs using **Silicon Motion (SMI)** controllers, as leaked or publicly available MP Tools are more common for this ecosystem. This is still **not guaranteed**.

---

⬅️ Prev: [High-Level Workflow](03-workflow.md)  
➡️ Next: [MP Tool Availability Assessment](05-mp-tool-availability.md)
