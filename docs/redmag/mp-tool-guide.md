<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# MP Tool Guide

## What MP Tools are

“MP” (Mass Production) tools are manufacturer utilities used to:
- initialize devices for shipment,
- configure NAND tables and firmware packages,
- set production parameters,
- run factory tests,
- modify identity fields and capacity profiles.

They operate at a low level and can permanently brick a drive if misused.

---

## Pre-flight checklist (do this every time)

- ✅ Confirm controller model
- ✅ Confirm NAND ID / vendor
- ✅ Confirm you have the correct tool family/version for that controller + NAND
- ✅ Use a known-good adapter
- ✅ Close other disk utilities (Disk Management, partition tools, etc.)
- ✅ Ensure stable power and cable connections
- ✅ Have a sacrificial test drive first

---

## Identifying controller and NAND (FLASH_ID)

With the SSD connected and recognized by Windows:

1. Download your FLASH_ID / SATA ID tool  
2. Run `sata_id.exe`  
3. Select the SSD when prompted  
4. Record:
   - controller model
   - NAND manufacturer
   - NAND ID

This information determines what MP tool versions are compatible.

---

## Finding the correct MP tool

This is often the most time-consuming step.

Typical sources:
- USBDEV
- Flashinfo
- LCB
- community research archives

Even when a tool exists, it may only support specific NAND revisions.

---

## Running the MP tool

### Antivirus warnings
MP tools often trigger antivirus because they access storage at a low level.
Use a controlled environment (test machine or isolated VM) and keep backups of tool archives.

### Connecting the SSD
- Connect via your adapter.
- If detection fails, some drives may require **ROM mode** (shorting specific pads). Not all drives need this.
- Click **Search** in the tool:
  - if the SSD appears correctly, the tool is likely compatible.
  - if it does not, you may have the wrong tool version.

---

## Configuring model and capacity (REDMAG requirements)

Once detected:

1. Open **Config**
2. Enter configuration password
   - for many SMI tools: **two spaces**
3. Change:
   - **Device Name / Model Number**
   - **Capacity**

### Model number
Must match a whitelisted RED string exactly.

### Capacity
Must match the selected RED model exactly.
In many SMI tools:
- choose `IDEMA`
- select an exact size from the dropdown

---

## Flashing

1. Save configuration
2. Return to main screen
3. Flash
4. Expect `PASS`

Errors may appear before completion, but bricking is still possible.
Never flash your only drive.

---

## Post-flash validation

- Unplug safely
- Reconnect and re-run identify tools
- Confirm model string and capacity are correct
- Only then install into the camera setup for validation testing
---

⬅️ Prev: [Capacity Overview](capacity-overview.md)  
➡️ Next: [Working Example](working-example.md)

