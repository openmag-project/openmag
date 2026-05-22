<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# Working Example

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

⬅️ Prev: [MP Tool Guide](05-mp-tool-guide.md)
