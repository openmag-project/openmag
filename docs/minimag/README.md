<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# openMAG MINIMAG Guide

### Table of Contents

- [Overview](01-overview.md)
- [SSD Guide](02-ssd-guide.md)
- [Hardware Guide](03-hardware-guide.md)
- [MINIMAG Validations Overview](04-minimag-validations-overview.md)
  - [Whitelist Overview](04a-whitelist-overview.md)
  - [Capacity Overview](04b-capacity-overview.md)
- [MP Tool Guide](05-mp-tool-guide.md)
- [Linux Sector Count Guide](06-linux-sector-count-guide.md)
- [Working Example](working-example.md)
- [Troubleshooting & Recovery](07-troubleshooting-and-recovery.md)
- [Quick Reference](08-quick-reference.md)

**Single-page version:** [full-content.md](full-content.md)

This guide ports the supplied 16-page `minimag-guide.pdf` into the same chapter-based reading path as the [REDMAG guide](../redmag/README.md). It documents the PDF's **480GB V1** profile and reported **DSMC2 v7.4.1** compatibility; it does not establish support for every SATA SSD or camera firmware. Start with the overview's scope and source notes.

### Source coverage

| PDF content | Pages | Repository chapter |
| --- | --- | --- |
| Purpose, MP tool explanation, compatibility and risk | 1–2 | [Overview](01-overview.md) |
| Hardware/software and drive requirements | 2–4, 16 | [SSD Guide](02-ssd-guide.md), [Hardware Guide](03-hardware-guide.md) |
| Controller/NAND/DRAM identification; package selection | 4–6 | [MP Tool Guide](05-mp-tool-guide.md) |
| Programming connection and ROM mode | 6–7 | [Hardware Guide](03-hardware-guide.md) |
| Identity fields, configuration figure, DRAM, programming | 7–11 | [Validations](04-minimag-validations-overview.md), [MP Tool Guide](05-mp-tool-guide.md) |
| Linux USB, HPA sector count, verification | 11–13 | [Capacity Overview](04b-capacity-overview.md), [Linux Sector Count Guide](06-linux-sector-count-guide.md) |
| Camera testing | 13 | [Working Example](working-example.md) |
| Troubleshooting and recovery | 14–15 | [Troubleshooting & Recovery](07-troubleshooting-and-recovery.md) |
| Cheat sheet, commands, links, requirements checklist | 15–16 | [Quick Reference](08-quick-reference.md) |

[Back to openMAG](../../README.md)
