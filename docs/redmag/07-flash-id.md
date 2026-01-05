# openMAG REDMAG Guide

**Educational & Research Documentation**

> ⚠️ **Disclaimer**  
> This guide is provided strictly for educational and research purposes.  
> Modifying SSD firmware using manufacturer production (MP) tools is inherently risky and can permanently damage hardware.  
> You assume all responsibility for any data loss, device failure, or equipment damage.  
>  
> This project is not affiliated with or endorsed by RED Digital Cinema.


---

## 4. Identifying Controller and NAND (FLASH_ID)

With the SSD connected and detected by Windows:

1. Download the **FLASH_ID / SATA ID tool**  
2. Run the `sata_id.exe`
3. Select the SSD when prompted
4. If successful, the tool will display:
   - Controller model
   - NAND manufacturer
   - NAND ID

This information is required to:
- Confirm MP Tool compatibility
- Select correct configuration parameters

---

⬅️ Prev: [Required Environment & Hardware](06-environment-hardware.md)  
➡️ Next: [Selecting the Correct MP Tool](08-mp-tool-selection.md)
