<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# Storage Hardware Deep Dive

This page is intentionally detailed. Most REDMAG “mystery failures” come down to one of these categories:

- protocol mismatch (SATA vs NVMe)
- connector/form-factor mismatch (microSATA vs mSATA vs 2.5" SATA)
- voltage mismatch (3.3V vs 5V)
- signal integrity / adapter issues
- SSD design choices (NAND type, DRAM cache, power-loss behavior)

## SATA protocol basics (what the camera expects)

SATA has multiple generations (commonly referred to as 1.5Gb/s, 3Gb/s, 6Gb/s). In practice:
- A newer SATA SSD will usually negotiate down to the link speed the host supports.
- Link negotiation issues can cause instability with marginal adapters or long cables.

REDMAG media presents a SATA device. **NVMe devices are not SATA devices**, even if the connector looks similar (M.2).

## Form factors and connectors

### microSATA (often found in early REDMAG units)
- Protocol: SATA
- Typical voltage: **3.3V**
- Connector: microSATA (compact SATA-style interface)
- Availability: scarce / discontinued for many models

Common modern workaround is an adapter to something more available. Adapters are a frequent source of freezes and dropouts.

### mSATA (recommended starting point)
- Protocol: SATA
- Typical voltage: **3.3V**
- Connector: mSATA edge connector (mini-card style)
- Availability: still commonly available

mSATA is generally the easiest path because it is:
- widely available
- natively 3.3V
- mechanically stable when mounted properly
- more often supported by identification/testing utilities

### 2.5" SATA SSD (electrically SATA, but power differs)
- Protocol: SATA
- Typical voltage: **5V**
- Connector: standard 7-pin data + 15-pin power
- Availability: abundant

2.5" SATA drives are SATA-compatible at the protocol level, but **not power-compatible** with a 3.3V-only supply.
If you want to use 2.5" SATA, you must provide stable external 5V power.

## Voltage is not optional

REDMAG/camera-side power is **3.3V**. Many SATA devices expect 5V.

- microSATA and mSATA: commonly **3.3V**
- 2.5" SATA: commonly **5V**

Power mismatch symptoms:
- camera freeze during media detect
- freeze during format
- intermittent disconnects while recording
- corrupted clips after offload

### Practical power rules
- Use the correct voltage for the SSD form factor.
- Use a clean, stable supply (not “whatever is nearby”).
- Avoid long, thin power leads that sag under load.
- Ensure a common ground between the camera data path and external power system.

> Placeholder: add measured current draw examples for common SSDs under sustained write.

## Signal integrity and why adapters can lock up the camera

SATA is sensitive to:
- cable quality and length
- connector tolerances
- impedance discontinuities introduced by cheap adapters
- power noise coupling into data lines

Common adapter-related failure modes:
- enumerates sometimes, not always
- works on a computer, freezes on the camera
- formats successfully, fails during recording
- works cold, fails warm (thermal expansion changes contact)

If you must use adapters:
- keep the data path short
- avoid stacking multiple adapters
- test with external power and a known-stable SATA cable first

## NAND types and why sustained writing matters

Cinema recording is mostly:
- long, continuous writes
- large sequential writes
- with bursts (start/stop, metadata, clip finalize)

NAND types:
- **SLC**: best endurance, rare/expensive
- **MLC**: excellent endurance and consistency (often ideal)
- **TLC**: common; quality varies; can work well if firmware is good
- **QLC**: typically poor sustained write behavior; **avoid for recording media**

A consumer SSD may advertise high burst speeds but collapse under sustained writes once its cache is exhausted.

## DRAM cache vs DRAM-less SSDs

DRAM in SATA SSDs is used for mapping tables and performance stability.
For cinema workloads, DRAM often helps with:
- consistent write latency
- avoiding sharp sustained-write drops
- faster metadata updates and FTL mapping

DRAM-less SATA SSDs can:
- feel “fine” in short tests
- but drop sharply during sustained recording
- or show unstable latency (risking dropped frames)

Recommendation:
- prefer SSDs with **onboard DRAM cache**, especially for longer takes

## Power-loss behavior (PLP) and safety

Many enterprise SSDs include **power-loss protection (PLP)** capacitors.
Consumer SSDs typically do not.

If power is lost mid-write:
- some SSDs recover cleanly
- others can corrupt the file system or internal mapping state

For camera media, PLP-like behavior is beneficial, but not required. If using consumer SSDs:
- avoid hot-unplug
- avoid unstable power sources
- keep the camera battery healthy

> Placeholder: add a page later listing SSD families known for stable sustained write behavior.



---

[← What is REDMAG?](01-what-is-redmag.md) | **Storage hardware deep dive** | [Validation model and whitelist →](03-redmag-validation-model.md)
