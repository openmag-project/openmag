<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# Quick Reference

## Reported 480GB profile

| Parameter | Value |
| --- | --- |
| Camera compatibility reported by source | DSMC2, firmware v7.4.1; dated March 2026 |
| Model Name | `RED 480GB V1` |
| Vendor Specific | `Red Digital ` — one trailing space |
| Serial format | `P1T1400508641101XXXX` — unique final four digits |
| SN Length | `20` |
| Reported Firmware Version | `0308-000` |
| Disk Size / selector | `Auto` / `Default` |
| Setting Capacity manually | Unchecked |
| Linux visible sector count | `937703088` |
| Logical sector size | `512` bytes |
| Total visible bytes | `480103981056` |

Serial and reported firmware requirements are not confirmed by the source. DRAM and NAND settings must match the actual SSD; do not copy them from the example screenshot.

---

## Linux commands

**Identify the drive first.** Replace `/dev/sdX` with the confirmed whole SSD device; never infer the target from size alone. Unmount its partitions and follow the full [Linux Sector Count Guide](06-linux-sector-count-guide.md) before changing capacity.

```sh
# Read-only identification and capacity inspection
lsblk -o NAME,MODEL,SERIAL,SIZE,LOG-SEC,MOUNTPOINTS
sudo hdparm -I /dev/sdX
sudo hdparm -N /dev/sdX
```

```sh
# Destructive-risk persistent capacity change: confirmed test SSD only
sudo hdparm -N p937703088 --yes-i-know-what-i-am-doing /dev/sdX
```

```sh
# Read back, then repeat after a full power cycle and re-identification
sudo hdparm -N /dev/sdX
```

---

## Workflow checklist

- [ ] Controller, NAND, and physical DRAM identified.
- [ ] Exact matching MP package and DRAM settings confirmed.
- [ ] Original identity recorded and all needed data backed up.
- [ ] Compatible SATA connection and stable power prepared.
- [ ] Identity set, Auto/Default capacity retained, configuration saved.
- [ ] Programming Pass and identity read-back recorded.
- [ ] Exact visible capacity verified before and after power removal.
- [ ] Camera recognition, in-camera format, long recordings, and computer playback tested.
- [ ] Results reported with camera firmware, recording settings, durations, and evidence.

---

## Source-listed software and references

- [SMI archive](https://usbdev.ru/files/smi/) — third-party package research lead from the PDF; no tools are bundled or endorsed here.
- [CrystalDiskInfo](https://crystalmark.info/en/software/crystaldiskinfo/).
- [Ubuntu Desktop](https://ubuntu.com/download/desktop).
- [Rufus](https://rufus.ie/).
- [balenaEtcher](https://etcher.balena.io/) — alternative USB writer mentioned by the source.
- [hdparm manual](https://man7.org/linux/man-pages/man8/hdparm.8.html) — supplemental reference for capacity semantics and command risks.

The source-to-chapter mapping is maintained in the [contents page](README.md).

---

Prev: [Troubleshooting & Recovery](07-troubleshooting-and-recovery.md)  
Next: [Contents](README.md)
