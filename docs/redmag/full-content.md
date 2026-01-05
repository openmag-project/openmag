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

## Overview

This guide documents the general research workflow used to prepare compatible SSD media for RED cameras by matching controller, NAND, and firmware configuration parameters to known, camera-recognized REDMAG profiles.

The process involves:
- Researching SSD hardware components
- Identifying compatible MP (Mass Production) tools
- Modifying SSD metadata at a low level
- Verifying functionality in supported RED cameras

This is **not** a guaranteed or supported process, and success varies significantly by controller, NAND, firmware revision, and tooling.

---

## High-Level Workflow

1. Research compatible SSD hardware  
2. Identify controller and NAND  
3. Locate and validate the correct MP Tool  
4. Prepare a Windows-based flashing environment  
5. Configure SSD identity and capacity  
6. Flash firmware/configuration  
7. Validate functionality in-camera  
8. Document results and iterate  

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

## 2. MP Tool Availability Assessment

Once the controller and NAND are known:

- Confirm that an appropriate MP Tool exists **before purchasing**
- Typical research sources include:
  - USBDEV
  - Flashinfo
  - LCB
  - Archived vendor tools
  - Community research posts

Finding the correct MP Tool is often the **most time-consuming step**.

> ⚠️ Even when an MP Tool exists, it may:
> - Only support specific NAND revisions
> - Require undocumented configuration
> - Fail silently or brick the SSD

---

## 3. Required Environment & Hardware

### Operating System
- **Windows is required**
  - MP Tools are Windows-only
  - Virtual machines are **not recommended** unless USB passthrough is proven stable

### Adapters
You will need an adapter to connect the SSD to your Windows machine:
- mSATA → USB
- microSATA → USB
- M.2 SATA → USB (ensure SATA, not NVMe)
- 2.5" SATA → USB

> USB adapters have proven reliable for MP Tool usage, but quality matters.

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

## 5. Selecting the Correct MP Tool

Using the confirmed controller and NAND data:

- Locate the closest matching MP Tool version
- Exact matches are preferred
- Minor NAND mismatches may still fail

> ⚠️ Expect trial and error.  
> Even with correct hardware, multiple MP Tool versions may need testing.

---

## 6. Running the MP Tool & Configuring the SSD

### Launching the MP Tool

1. Run the MP Tool executable
2. Expect antivirus warnings  
   - These tools access storage at a very low level
   - False positives are common

### Connecting the SSD

- Connect the SSD via USB adapter
- If the drive is not detected:
  - You **may** need to place the SSD into **ROM mode**
  - This typically involves shorting two test pads on the PCB
  - Not all SSDs require this

### Verifying Detection

- Click **Search** in the MP Tool
- The SSD must appear correctly in the device list
- If it does not, the MP Tool is likely incompatible

---

## 7. MP Tool Configuration

Once the SSD is detected:

1. Open **Config**
2. Enter the configuration password  
   - For many SMI tools, this is **two spaces**
3. Editable fields will unlock

### Required Configuration Changes

#### Device Name / Model Number
- Must exactly match a **RED-whitelisted model**
- Case, spacing, and formatting must be perfect

### Whitelist Reference

Complete list of supported model names from DSMC firmware. **Copy these EXACTLY - spacing and capitalization matter!**
#### Smallest Capacities

```
RED 16GB REV B
RED 32GB REV A1
RED 64GB REV A1
RED 55GB V1
RED 55GB V2
```

#### 64GB Models (Note: TWO spaces before "64")

```
RED  64GB Rev T1
RED  64GB Rev T2
RED  64GB Rev T3
```

#### 128GB Models

```
RED 128GB Rev T1
RED 128GB Rev T2
RED 128GB Rev T3
```

#### 256GB Models (Recommended)

```
RED 256GB Rev T1
RED 256GB Rev T2
RED 256GB Rev T3
```

#### 512GB Models (Maximum Capacity)

```
RED 512GB V1
RED 512GB V2
RED 512GB V3
RED 512GB V4
```

### SSDs (SSD Designation)

**Note: These have "SSD" suffix and different spacing**

```
RED 55GB SSD 
RED 64GB SSD 
RED 128GB SSD 
RED 256GB SSD 
RED 512GB SSD 
```

**Note:** Some have trailing space after "SSD" - include it!

### CompactFlash Cards

```
RED 16GB CF
RED 32GB CF
RED 64GB CF
LEXAR ATA FLASH CARD
```

**Note:** CF cards are obsolete format, not recommended for new projects

### Recommended Models for DIY

**Best choices for generic SSD conversion:**

**For 256GB drive:**
```
RED 256GB Rev T3    ← Newest revision (recommended)
RED 256GB Rev T2
RED 256GB Rev T1
RED 256GB SSD       ← SSD variant (not tested yet)
```

**For 512GB drive (maximum):**
```
RED 512GB V4        ← Newest revision (recommended)
RED 512GB V3
RED 512GB V2
RED 512GB V1
RED 512GB SSD       ← SSD variant (not tested yet)
```

**For 128GB drive:**
```
RED 128GB Rev T3    ← Newest revision (recommended)
RED 128GB Rev T2
RED 128GB Rev T1
RED 128GB SSD       ← SSD variant (not tested yet)
```

### Spacing Reference

**CRITICAL:** Some models have unusual spacing!

**64GB models (TWO spaces):**
```
RED  64GB Rev T1
RED  64GB Rev T2
RED  64GB Rev T3
   ↑↑ TWO spaces between RED and 64
```

**All other capacities (ONE space):**
```
RED 128GB Rev T1
RED 256GB Rev T1
RED 512GB V1
   ↑ ONE space between RED and capacity
```

**To verify your spacing:**
```
Wrong: RED 64GB Rev T1   (one space - will fail!)
Right: RED  64GB Rev T1  (two spaces - will work!)
```

#### Capacity
- Must match the selected RED model exactly. Example, if you are using `RED 512GB V4` your capacity MUST be 512GB.
- In SMI tools:
  - Select `IDEMA`
  - Choose the exact capacity from the dropdown

---

## 8. Flashing the SSD

1. Save the configuration
2. Return to the main MP Tool screen
3. Select **Flash**

### Expected Results

- **PASS** indicates a successful operation
- Errors may appear before flashing completes
- Failure does **not** always prevent bricking

> ⚠️ There is always a non-zero risk of permanent failure.

---

## 9. Camera Validation

1. Disconnect the SSD from the USB adapter
2. Install it onto the RED PCB
3. Insert into the camera
4. Power on and test

### Success Criteria

- No “Unauthorized Media” warning
- Media formats successfully
- Stable recording behavior

---

## 10. Next Steps & Future Work

### Hardware & Enclosures
- Design and 3D print SSD enclosures
- Standardize a reusable RED-compatible PCB
- Reduce cost to:
  - PCB
  - SSD
  - Printed enclosure

### Documentation
- Maintain a public list of:
  - Verified SSDs
  - Controller + NAND combinations
  - Working MP Tools
- Complete the **MINIMAG guide**

### Education
- Produce a full video walkthrough
- Expand SSD selection criteria for cinema use:
  - Sustained write performance
  - Thermal stability
  - Power characteristics
  - Controller behavior under load

---

## Closing Notes

This process blends hardware research, firmware tooling, and controlled experimentation.  
Patience, documentation, and risk awareness are essential.

**Never test on your only SSD.**
