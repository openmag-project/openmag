<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# Hardware Guide

## Bench requirements

- Windows PC with administrator access; the source recommends Windows 10 or 11 for its Windows-only MP utilities.
- Compatible SATA SSD and an adapter that passes the tool's low-level ATA commands.
- Stable power, secure connectors, and a backup of any data on the SSD.
- Linux machine, or a spare **8GB or larger USB stick** for a live Ubuntu environment.
- DSMC2 camera and a MINI-MAG enclosure/adapter for final testing.

Creating a bootable USB erases that USB stick. Programming and camera formatting erase the test SSD. Identify each device before performing those operations.

---

## Adapter selection

The source reports these options:

1. **Direct motherboard SATA** through an mSATA-to-SATA or M.2 SATA-to-SATA adapter: its preferred connection for raw command access.
2. **USB-C MINI-MAG REDSTATION**: reported working for MP programming in the source, without an exact hardware revision or chipset.
3. **USB SATA dock**: dependent on the bridge and command passthrough. UASP or SAT support alone does not establish MP-tool or HPA support.

An adapter working for ordinary file transfers does not prove it supports programming, ROM-mode detection, or HPA commands. Those stages may need different connections. Record the adapter model and interface used at each stage.

---

## Connect for programming

1. For motherboard SATA, shut down and disconnect power before installing the SSD and adapter.
2. Seat and secure the SSD, then connect the adapter to the host.
3. Boot Windows, or connect the USB adapter as appropriate.
4. Confirm the intended SSD appears in **Device Manager > Disk drives**.
5. Cancel any Windows request to initialize the disk. Do not partition or format it for the MP tool.
6. Close Disk Management, CrystalDiskInfo, and other disk utilities before programming.

Use a direct port and stable power. If using a virtual machine, document the hypervisor and passthrough setup; disconnects can interrupt programming.

---

## ROM / ISP recovery mode

Some drives that cannot be detected normally may require ROM mode, also called ISP or safe mode. Try normal detection first.

Only use recovery pads documented for the **exact SSD model and PCB revision**. Disconnect power before attaching a jumper to those designated pads, then follow the board-specific instructions for applying power and releasing the jumper after detection. Pad locations and timing are not universal. Do not guess based on another board's photograph.

The source describes temporarily shorting documented ROM pads during power-up and releasing the short after the MP tool detects the controller. This is a recovery technique, not a prerequisite for every drive. Recovery is not guaranteed; see [Troubleshooting & Recovery](07-troubleshooting-and-recovery.md).

---

## Software to prepare

- [CrystalDiskInfo](https://crystalmark.info/en/software/crystaldiskinfo/) for reported model, serial, and firmware. These fields can suggest hardware but do not reliably identify every controller, NAND, or DRAM chip.
- A controller/NAND-matched MP tool package; see [MP Tool Guide](05-mp-tool-guide.md).
- [Ubuntu Desktop](https://ubuntu.com/download/desktop), with [Rufus](https://rufus.ie/) or [balenaEtcher](https://etcher.balena.io/) to create a live USB if needed.
- Linux `hdparm` for the separate capacity step.

No firmware binaries or MP tool executables are included in this repository. Follow the repository's [contribution rules](../../CONTRIBUTING.md) when sharing research.

---

Prev: [SSD Guide](02-ssd-guide.md)  
Next: [MINIMAG Validations Overview](04-minimag-validations-overview.md)
