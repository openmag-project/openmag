<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# SSD Guide

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

⬅️ Prev: [Overview](01-overview.md)  
➡️ Next: [Hardware Guide](03-hardware-guide.md)
