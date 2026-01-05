<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

## Identifying Controller and NAND

It's recommended you download the SMI Flash ID tool. This will scan your connected SSD and show the Controller, NAND, Firmware, and other info. Very helpful. You can download this tool here:

http://vlo.name:3000/ssdtool/

Look for SMI flash id (PATA,SATA,CF,SD) under the SMI Utility section.

With the SSD connected and detected by Windows:

1. Run the SMI Flash Tool (sata id)
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
