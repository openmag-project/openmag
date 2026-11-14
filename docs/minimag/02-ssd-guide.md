<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# SSD Guide

## Supported hardware for this workflow

The source covers **Silicon Motion (SMI)** controllers such as SM2246EN, SM2258, and SM2259. A controller family name alone does not establish compatibility: the MP tool package must support the exact controller **and NAND combination**.

Other controller families, including Phison, Maxio, and Realtek, are mentioned in the PDF but are outside its worked procedure. Do not substitute their tools or settings into this workflow.

---

## Controller, NAND, and DRAM

An SSD contains several components that must be identified before programming:

- **Controller**: runs the firmware and manages communication and flash storage.
- **NAND flash**: stores the data; record the complete package part number and detected flash ID when available.
- **DRAM**: working memory used by the controller; record manufacturer, capacity, memory generation, and rated clock.

The PDF requires a physical DRAM chip and excludes DRAM-less/XT variants from its workflow. Confirm the actual hardware revision through chip markings, datasheets, or a documented teardown. A small chip's location or shape alone is insufficient identification.

DRAM presence does not guarantee sustained recording performance. Controller firmware, NAND, cache exhaustion, temperature, and power also affect results. The source's approximately **300 MB/s sustained** target is a screening guideline, not a verified requirement for every camera mode; it suggests looking for **400+ MB/s sustained** when performance is insufficient.

---

## Form factor and capacity

- **mSATA**: the source describes this as the original 480GB V1 MINI-MAG's internal form factor.
- **M.2 SATA**: requires a compatible M.2-to-mSATA adapter and enough physical space in the enclosure.
- **M.2 NVMe**: outside this workflow; PCIe/NVMe is not SATA. Check the interface specification rather than relying on connector keying alone.

The drive must natively expose at least **937,703,088 sectors of 512 bytes** after programming. HPA can hide capacity; it cannot create storage on a smaller drive. A model label or retail capacity is not enough to verify this requirement.

---

## Candidate checklist

- [ ] Controller and exact NAND identified.
- [ ] Matching MP tool package available before buying or programming.
- [ ] Physical DRAM present and its configuration known.
- [ ] SATA interface and a suitable enclosure/adapter.
- [ ] Sufficient native capacity for the 480GB profile.
- [ ] Sustained write performance tested beyond cache exhaustion and at operating temperature.
- [ ] Long recordings and read-back verification planned for the intended camera mode.

For more background on NAND, caching, and sustained writes, see the [REDMAG SSD Guide](../redmag/02-ssd-guide.md). Its general SSD concepts apply; its REDMAG identity and capacity settings do not replace the MINIMAG profile here.

---

Prev: [Overview](01-overview.md)  
Next: [Hardware Guide](03-hardware-guide.md)
