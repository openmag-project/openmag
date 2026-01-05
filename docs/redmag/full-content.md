<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# openMAG REDMAG Guide

## Goal

The goal of this REDMAG guide is to document—clearly and thoroughly—how REDMAG media behaves from the perspective of:

1. **SSD internals** (controller, NAND, firmware, DRAM, power behavior)  
2. **RED camera validation** (what the camera checks, and why mismatches fail)  
3. **Tooling and workflow** (how researchers identify components, choose tools, and validate results)  
4. **Repeatable research reporting** (how to capture evidence and share findings responsibly)

This is intended to be a practical, engineering-focused guide you can follow end-to-end.

---

## Problem Statement (rolled into the overview)

DSMC1-era RED cameras using **REDMAG** media rely on firmware-level validation to determine whether attached SSD media is “recognized” and allowed for recording. These checks prevent many generic SATA SSDs from being accepted, even when the underlying hardware can sustain recording bandwidth.

As official REDMAG media becomes increasingly scarce, expensive, or discontinued, users maintaining legacy systems need a structured way to:

- understand the requirements,
- test candidates safely,
- document results accurately.

---

## What REDMAG validation checks (observed)

Through firmware analysis and hands-on testing, REDMAG acceptance is observed to depend primarily on **two values**:

- **SSD Model Number** (ATA Identify “Model” string)
- **Reported Capacity** (logical addressable capacity exposed by the SSD)

The camera firmware extracts capacity encoded in the model string (e.g., “256GB”) and compares it to the drive’s reported capacity. These must match exactly.

Key observations:

- REDMAG does **not** validate `0x90h` / `0x91h` style fields (those are MINIMAG-related).
- Camera-side **power is not required** for basic SATA identity detection (data only can be sufficient), though most real setups use camera power.
- Exact **spacing and capitalization** of model strings matters.

---

## Guide map

- **SSD Guide**: deep SSD anatomy + what makes a “cinema-friendly” SSD  
- **Hardware Guide**: adapters, cables, power, and bench setup that prevents false failures  
- **REDMAG Validations Overview**: the camera’s decision logic (whitelist + capacity)  
- **MP Tool Guide**: how researchers identify controller/NAND, select tools, configure, and flash  
- **Working Example**: a documented test case with screenshot placeholders

---

## SSD Anatomy (what matters for REDMAG research)

A SATA SSD is a complete embedded system that presents storage over the SATA protocol. For REDMAG research, the most important internal layers are:

- **Controller (SoC)**: runs the Flash Translation Layer (FTL), error correction (ECC), wear leveling, garbage collection, SATA command handling (NCQ), and power management.
- **NAND flash**: non-volatile storage; requires complex management (erase-before-write, block wear, bad block handling).
- **DRAM (optional)**: stores mapping tables and buffers; improves consistency for mixed workloads; some drives are DRAM-less.
- **Firmware + configuration**: often includes per-NAND timing tables, channel configuration, overprovisioning, and identity strings.
- **Power regulation**: converts input rails to what the controller/NAND need; instability here causes resets or corruption.

---

## Controller details (why the controller is the “personality”)

The controller strongly influences:
- sustained write stability (long continuous writes),
- behavior when SLC cache is exhausted,
- thermal throttling strategy,
- garbage collection aggressiveness,
- recoverability after errors,
- tool ecosystem availability (diagnostic tools, MP tools, community knowledge).

### What to capture about a controller
- Vendor + model family (e.g., Silicon Motion SM2258/SM2259, etc.)
- Reported firmware version (ATA Identify)
- Whether it’s known to have accessible MP tools
- Any known quirks (capacity rounding, power state behavior)

---

## NAND types (SLC / MLC / TLC / QLC) and cinema relevance

**Bit-per-cell types**
- **SLC (1 bit)**: fastest, best endurance, rare and expensive.
- **MLC (2 bit)**: strong endurance; mostly older drives.
- **TLC (3 bit)**: common; quality varies widely.
- **QLC (4 bit)**: highest density; often poor sustained write once cache is exhausted.

**Cinema takeaway:** TLC can be great if the controller and firmware manage cache/GC well; QLC is often risky for long sustained recording.

### 3D NAND vs planar
- 3D NAND dominates modern production and tends to have different thermal and latency behavior.
- Planar NAND is mostly older and sometimes behaves more predictably under sustained load, depending on controller/firmware.

---

## DRAM vs DRAM-less (predictability matters)

DRAM is commonly used for the address mapping table (L2P mapping).
- **With DRAM**: better sustained random behavior, fewer surprise stalls, improved consistency during garbage collection.
- **DRAM-less**: can be fine for sequential writes but may show sudden pauses under mapping pressure.

**Cinema takeaway:** prefer DRAM drives when possible for consistent latency.

---

## SLC cache behavior (the most common cinema failure mode)

Most modern TLC/QLC drives accept writes into a fast SLC cache first.
When the cache fills:
- sustained write speed can drop sharply,
- latency can spike,
- firmware may pause to fold SLC data back into TLC/QLC (background work).

**Research question to answer:**
> What is the *worst-case sustained write rate* after cache exhaustion at operating temperature?

---

## Firmware, overprovisioning, and why “capacity” can be tricky

SSDs typically reserve hidden space for:
- bad block replacement,
- wear leveling,
- garbage collection,
- SLC caching.

This is **overprovisioning**. Good for endurance—but can create subtle issues if reported user capacity is non-standard or rounded differently.

When documenting a drive:
- record reported LBAs / sectors,
- record sector size,
- record “user capacity” outputs in multiple tools.

---

## What makes an SSD good for cinema (practical checklist)

A cinema-friendly SSD is:
- **stable** under long continuous writes,
- **thermally predictable** in an enclosed housing,
- **low-latency** without periodic stalls,
- **power tolerant** (doesn’t brownout or reset under bursts),
- **recoverable** (doesn’t enter bad states after errors).

### Suggested evaluation approach (bench)
- sustained write tests beyond cache size,
- “warm” tests (after pre-heating the drive),
- long sequential write + read-back verification,
- repeat tests across multiple runs.

### Suggested evaluation approach (in-camera)
- repeated long clips at highest bitrate settings you use,
- observe for periodic stalls,
- verify format/verify cycles,
- test multiple power cycles.

---

## Goal of the hardware setup

Your test bench should make failures attributable. Many “SSD failures” are actually caused by:
- unstable USB adapters,
- poor cables,
- insufficient power,
- bad USB hubs,
- flaky USB passthrough in virtual machines.

If you want repeatable results, make the bench boring and stable.

---

## Host machine guidance

- Windows is commonly used for MP tools and some vendor utilities.
- Prefer a direct USB port on the machine (avoid front-panel ports and hubs).
- Keep the environment consistent: same OS build, same drivers, same adapter.

### Virtual machines
VMs can work, but they introduce risk:
- USB passthrough disconnects,
- timing differences,
- bridge resets during low-level operations.

If you use a VM, document it explicitly (hypervisor, passthrough method).

---

## Adapter guidance by form factor

You may need:
- **mSATA → USB**
- **microSATA → USB**
- **M.2 SATA → USB** *(verify adapter supports SATA, not NVMe-only)*
- **2.5\" SATA → USB**

### What makes a good adapter
- stable under sustained writes,
- no disconnects during identify or flash operations,
- consistent sector reporting,
- reliable chipset.

**Document your adapter:** model, chipset if known, and any quirks.

---

## Power and cabling

### Power stability
Low-level operations can stress a drive:
- higher write bursts,
- firmware transitions,
- internal GC spikes.

Ensure:
- adequate USB power (avoid weak ports),
- use externally powered enclosures if needed,
- short, high-quality cables.

### Cabling
- Use short USB cables.
- Avoid “charge-only” or thin cables.
- For microSATA, avoid flexing the connector.

---

## Optional but useful bench items

- ESD mat / wrist strap (protects small PCBs)
- A dedicated label system (drive ID, date, state)
- A small bench PSU for repeatable power testing
- IR thermometer or thermal probe (capture operating temperature)
- A “known good” reference SSD and adapter pair

---

## Camera-side considerations

- If you test with camera power, document:
  - camera model,
  - firmware version,
  - battery type / external power,
  - any additional modules in the chain.

Even when SATA identity reads work on data-only, real-world recording reliability should be tested with the full camera setup you intend to use.

---

## What validation means

In this context, “validation” is the camera’s decision-making process for whether a media device is:
- recognized,
- allowed to format,
- allowed to record without warnings.

Different media families can have different validation depth. REDMAG is observed to be simpler than MINIMAG.

---

## REDMAG validation model (observed)

Observed inputs:
1. **Model Number** (ATA Identify “Model” string)
2. **Reported capacity** (sector count × sector size)

Observed logic:
- Parse the capacity encoded in the model string (e.g., “256GB”).
- Compare to the SSD’s reported capacity.
- Require exact match (practically: no mismatch tolerated).

If the model string is not recognized (whitelist mismatch), or capacity doesn’t match expectations, the camera warns or rejects the media.

---

## What to document during validation research

For every test run, capture:

### Identity
- Exact model string **including spaces**
- Firmware version reported by the drive
- Serial number (optional, for tracking, not for authenticity claims)

### Capacity
- Total LBAs / sectors
- Logical sector size
- Reported “user capacity” in bytes (from a tool)
- Any adapter-specific reporting behavior

### Camera behavior
- Warning messages verbatim
- Ability to format
- Recording stability under longest clip you tested

---

## This section’s subpages

- [Whitelist Overview](whitelist-overview.md)
- [Capacity Overview](capacity-overview.md)

---

## Whitelisted REDMAG model numbers

These model numbers were extracted from DSMC firmware and verified through testing.

**IMPORTANT:** Copy these **exactly**. Spacing, capitalization, and even trailing spaces can matter.

---

## Smallest capacities

```
RED 16GB REV B
RED 32GB REV A1
RED 64GB REV A1
RED 55GB V1
RED 55GB V2
```

---

## 64GB models (TWO spaces before “64”)

```
RED  64GB Rev T1
RED  64GB Rev T2
RED  64GB Rev T3
```

---

## 128GB models

```
RED 128GB Rev T1
RED 128GB Rev T2
RED 128GB Rev T3
```

---

## 256GB models (recommended)

```
RED 256GB Rev T1
RED 256GB Rev T2
RED 256GB Rev T3
```

---

## 512GB models (maximum)

```
RED 512GB V1
RED 512GB V2
RED 512GB V3
RED 512GB V4
```

---

## “SSD” designation models

**Note:** These include an `SSD` suffix and may include a trailing space after `SSD`.

```
RED 55GB SSD 
RED 64GB SSD 
RED 128GB SSD 
RED 256GB SSD 
RED 512GB SSD 
```

---

## CompactFlash (legacy)

```
RED 16GB CF
RED 32GB CF
RED 64GB CF
LEXAR ATA FLASH CARD
```

---

## Recommended models for DIY conversions

These are the most practical targets based on common capacities and “newest” revisions:

### 256GB
```
RED 256GB Rev T3    ← Newest revision (recommended)
RED 256GB Rev T2
RED 256GB Rev T1
RED 256GB SSD       ← SSD variant (not tested yet)
```

### 512GB
```
RED 512GB V4        ← Newest revision (recommended)
RED 512GB V3
RED 512GB V2
RED 512GB V1
RED 512GB SSD       ← SSD variant (not tested yet)
```

### 128GB
```
RED 128GB Rev T3    ← Newest revision (recommended)
RED 128GB Rev T2
RED 128GB Rev T1
RED 128GB SSD       ← SSD variant (not tested yet)
```

---

## Spacing reference (critical)

**64GB models use TWO spaces between `RED` and `64`:**
```
RED  64GB Rev T1
RED  64GB Rev T2
RED  64GB Rev T3
   ↑↑ TWO spaces between RED and 64
```

**All other capacities use ONE space:**
```
RED 128GB Rev T1
RED 256GB Rev T1
RED 512GB V1
   ↑ ONE space between RED and capacity
```

**Verify your spacing:**
```
Wrong: RED 64GB Rev T1   (one space - will fail!)
Right: RED  64GB Rev T1  (two spaces - will work!)
```

---

## What “capacity” means to a camera

At the device level, capacity is usually expressed as:
- total logical sectors (LBAs),
- logical sector size (commonly 512 bytes),
- total user addressable bytes = LBAs × sector size.

Many tools also show:
- “user capacity” in bytes,
- nominal marketing size (GB),
- binary size (GiB).

For REDMAG, the camera expects the **capacity embedded in the model string** to match the device’s **reported capacity**.

---

## Why exact matches matter

Observed behavior indicates that the firmware:
- extracts the numeric capacity token (e.g., 256GB),
- compares it to the SSD’s reported capacity,
- requires exact matching.

This is why:
- a correct model string with incorrect reported capacity fails,
- a correct capacity with an unrecognized model string fails.

---

## Common mismatch causes

- Using the wrong capacity selector in an MP tool (e.g., not selecting IDEMA)
- Bridge adapters that misreport sector counts
- Firmware-level overprovisioning being exposed incorrectly
- Decimal vs binary confusion when humans eyeball results (the camera uses the real numbers)

---

## What to record in your notes

Capture:
- total LBAs/sectors from Identify Device,
- logical sector size,
- reported bytes from at least one tool,
- camera behavior (format/record).

A good habit is to paste tool output into your notes so spacing and numbers are preserved.

---

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

## Goal

This page shows a step-by-step working example and a format for documenting results. Replace placeholders with your real screenshots and notes.

---

## Example scenario

Target: create a 256GB REDMAG-compatible SSD profile.

### Bench details
- Date: YYYY-MM-DD
- Camera: (Scarlet-X / EPIC-X / etc.)
- Camera firmware: (version)
- SSD: (retail model)
- Form factor: mSATA
- Adapter: mSATA → USB
- Host OS: Windows (version/build)

---

## Step-by-step

### 1) Identify controller and NAND (FLASH_ID)

- Connect SSD via adapter
- Run `sata_id.exe`
- Select SSD and record controller + NAND IDs

**Screenshot:**  
![FLASH_ID Output](assets/screenshots/01-flash-id-output.png)

---

### 2) Select MP tool

- Use controller + NAND IDs to select a matching MP tool version
- Launch tool and click **Search** to confirm the device appears

**Screenshot:**  
![MP Tool Detection](assets/screenshots/02-mp-tool-detection.png)

---

### 3) Configure model number and capacity

- Open Config
- Password: (for many SMI tools: two spaces)
- Set model:
  - `RED 256GB Rev T3`
- Set capacity:
  - 256GB (IDEMA / exact selection)

**Screenshot:**  
![MP Tool Config](assets/screenshots/03-mp-tool-config.png)

---

### 4) Flash

- Save config
- Flash
- Confirm `PASS`

**Screenshot:**  
![Flash PASS](assets/screenshots/04-flash-pass.png)

---

### 5) Validate in camera

- Install onto REDMAG PCB
- Insert into camera
- Confirm:
  - no unauthorized media warning
  - formats successfully
  - stable recording

**Screenshot:**  
![Camera Media Screen](assets/screenshots/05-camera-media.png)

---

## Results summary (fill this in)

- Status: PASS / FAIL / PARTIAL / NEEDS RETEST
- Notes:
- Longest clip tested:
- Any stalls or warning messages:
- Next experiments:

---

## Screenshot directory layout

```
assets/
  screenshots/
    01-flash-id-output.png
    02-mp-tool-detection.png
    03-mp-tool-config.png
    04-flash-pass.png
    05-camera-media.png
```
---

⬅️ Prev: [Contents](README.md)

