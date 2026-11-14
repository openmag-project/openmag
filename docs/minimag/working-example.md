<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# Working Example

## Goal

Follow the source's 480GB profile and record reproducible results. **This page is a worksheet, not a new independently verified openMAG hardware test.** The PDF provides a configuration figure but no complete drive identification, camera logs, or recording-duration results for this port to reproduce.

---

## Bench details (fill in before testing)

| Item | Your test record |
| --- | --- |
| Date / researcher | To record |
| Camera / firmware | To record; source reports DSMC2 v7.4.1 |
| SSD retail model / PCB revision | To record |
| Controller / NAND part number and ID | To record |
| DRAM manufacturer / part / size / type / clock | To record |
| Native sectors / logical sector size | To record |
| Adapter for MP programming / Linux HPA | To record separately |
| Windows / Linux versions | To record |
| MP tool package / version / saved config | To record |

---

## 1) Identify the SSD and select a tool

Record the original identity, inspect controller/NAND/DRAM, and match the MP package to that hardware. Save identification output and chip photographs with your test notes. Follow [MP Tool Guide](05-mp-tool-guide.md), Steps 1–3.

## 2) Configure the profile

Set model `RED 480GB V1`, vendor `Red Digital ` with its trailing space, reported firmware `0308-000`, and your unique 20-character serial. Leave capacity on Auto/Default with manual capacity unchecked. Configure DRAM from the actual chip specifications.

Review the [source configuration figure](assets/screenshots/01-mp-tool-parameters.png) for field locations, while using your own hardware's NAND and DRAM values. Save the configuration before starting.

## 3) Program and verify identity

Run the tool, wait for Pass, and reconnect the SSD. Record the resulting model, serial, and reported firmware. Save the tool log and configuration; a successful programming result is only one stage of the test.

## 4) Set and verify capacity

Follow the [Linux Sector Count Guide](06-linux-sector-count-guide.md). Record visible/native counts before and after the change and again after a full power cycle. Require `937703088` visible 512-byte sectors.

## 5) Test in camera

1. With the equipment powered down, install the mSATA SSD in the MINI-MAG enclosure, or install the SATA M.2 drive through a suitable adapter. Seat and secure all connections.
2. Insert the assembled media into the DSMC2 camera and power on.
3. Check media status. The source reports an **S-SSD** display near **447.1 GiB**.
4. Format in camera; the source gives **Menu > Media > Format**, though menu labels may vary. Formatting erases existing content.
5. Record a short clip at a moderate data rate, then progressively test the highest settings you intend to use.
6. Watch for **Media too slow**, **Dropped frames**, and **Unsupported media** warnings; copy any messages verbatim.
7. Record several long clips beyond the SSD's fast-cache capacity. Play back and inspect footage on a computer, and repeat after power cycles and at operating temperature.

Do not infer recording reliability from an accepted identity, a successful format, or a short clip. Preserve the actual duration, settings, and observed limits of each test.

---

## Results summary (fill in)

- Status: **NOT TESTED / PASS / FAIL / PARTIAL / NEEDS RETEST**
- Identity verification:
- Visible/native sector counts and persistence:
- Camera recognition / format result:
- Resolution / frame rate / compression / data rate:
- Longest clip and total recorded duration:
- Temperature and power conditions:
- Warnings, stalls, or interruptions:
- Computer playback / read-back result:
- Evidence filenames and next experiments:

Keep your own screenshots and logs alongside the test report. No placeholder image links are included as if evidence already exists.

---

Prev: [Linux Sector Count Guide](06-linux-sector-count-guide.md)  
Next: [Troubleshooting & Recovery](07-troubleshooting-and-recovery.md)
