<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# MP Tools Overview (General and Vendor-Agnostic)

This section explains MP tools in depth **without providing REDMAG-specific circumvention instructions**.

MP (Manufacturing Process) tools are factory provisioning utilities used to configure SSD controllers and NAND during manufacturing.
They can expose knobs consumer utilities do not.

## What MP tools can control (general)

Depending on controller family, MP tools may allow:
- factory formatting / NAND provisioning
- configuration of over-provisioning
- setting identity strings and firmware parameters
- internal self-tests and burn-in routines

## Why matching an MP tool is difficult

MP tools are typically specific to:
- controller family (example: Silicon Motion, Phison, Marvell, etc.)
- controller revision/stepping
- NAND vendor + process generation
- firmware branch

A wrong match can permanently brick the SSD.

## How engineers identify the hardware (read-only methods)

Common approaches in general SSD engineering include:

1. **Physical inspection**
   - open the enclosure (if accessible)
   - read the controller package marking
   - read NAND package markings

2. **Controller identification from software**
   - read SATA identify fields (model, firmware)
   - use SMART and vendor log pages (where available)
   - use PCI/USB bridge IDs if the SSD is behind an adapter (limited usefulness)

3. **Cross-referencing public sources**
   - SSD teardowns
   - controller datasheets
   - community-maintained component databases

## What to look for when choosing a tool (conceptual checklist)

- Does the tool explicitly list your controller family and revision?
- Does it support your NAND vendor/type?
- Does it support the target capacity class?
- Do you have evidence (photos/logs) that the tool worked with your exact SSD revision?
- Does the tool provide a safe “identify-only” mode for verification before any write operation?

## Practical guidance for beginners

- Treat MP tools as “factory-grade” tooling, not consumer software.
- Assume documentation is incomplete.
- Assume mistakes are irreversible.
- Prioritize SSDs with a track record of stable sustained writes and known components.

openMAG’s goal is to:
- document compatibility findings
- teach the concepts
- provide repeatable validation procedures

> Placeholder: add a generic example walkthrough that demonstrates *identification* and *tool selection* using a non-camera SSD scenario,
> without including modification steps.



---

[← End-to-end workflow](05-high-level-process.md) | **MP Tools overview** | [Adapters and power →](07-adapters-and-power.md)
