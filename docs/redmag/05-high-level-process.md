<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# End-to-End Workflow (Safe and Repeatable)

This workflow is designed for beginners. It is intentionally structured to reduce risk to your camera and footage.

## What you need (high level)

- A known-good REDMAG (baseline)
- Your candidate SSD
- A way to connect the SSD to a computer for read-only inspection (SATA/mSATA adapter, enclosure, etc.)
- A stable power strategy (especially if using anything that requires 5V)

## Step 1: Establish a baseline

1. Insert your known-good REDMAG.
2. Confirm the camera:
   - detects the media
   - formats successfully (if you choose to reformat)
   - records a short clip
   - offloads a clip successfully

Record:
- camera model
- camera firmware version
- the REDMAG model name shown (camera UI or host system)

## Step 2: Inspect your candidate SSD (read-only)

On a computer, collect:
- model string
- firmware version
- reported capacity
- SMART health data (if available)

Do not write anything to the SSD at this stage.

> Placeholder: add platform-specific quickstart (Windows/macOS/Linux).

## Step 3: Build a stable test bench

Goal: eliminate variables.

- Keep the SATA data path short and consistent.
- Avoid stacking adapters.
- If using a 2.5" SATA SSD, supply stable external 5V power.
- Ensure common ground between power and data paths.

## Step 4: Camera validation sequence (repeat every time)

After any change (or when testing a new physical configuration), use the same sequence:

1. Insert media and confirm detection
2. Format in-camera
3. Record a short clip (sanity test)
4. Record a longer clip (stress test)
5. Offload the clips
6. Verify integrity (checksum compare if possible)
7. Repeat after a reboot (consistency test)

## Step 5: Document your results

For community usefulness, include:
- exact SSD model and revision (photos help)
- controller and NAND IDs (if known)
- adapter and power details
- camera model + firmware version
- what tests passed/failed

This is what turns one person’s success into repeatable knowledge.



---

[← Recording restrictions](04-recording-restrictions.md) | **End-to-end workflow** | [MP Tools overview →](06-mp-tools-overview.md)
