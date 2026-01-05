<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# Hardware Guide

## Goal of the hardware setup

Your test bench should make failures attributable. Many “SSD failures” are actually caused by:
- unstable USB adapters,
- poor cables,
- insufficient power,
- bad USB hubs,
- flaky USB passthrough in virtual machines.

If you want repeatable results, make the bench boring and stable.

---

## Host machine guidance

- Windows is commonly used for MP tools and some vendor utilities.
- Prefer a direct USB port on the machine (avoid front-panel ports and hubs).
- Keep the environment consistent: same OS build, same drivers, same adapter.

### Virtual machines
VMs can work, but they introduce risk:
- USB passthrough disconnects,
- timing differences,
- bridge resets during low-level operations.

If you use a VM, document it explicitly (hypervisor, passthrough method).

---

## Adapter guidance by form factor

You may need:
- **mSATA → USB**
- **microSATA → USB**
- **M.2 SATA → USB** *(verify adapter supports SATA, not NVMe-only)*
- **2.5\" SATA → USB**

### What makes a good adapter
- stable under sustained writes,
- no disconnects during identify or flash operations,
- consistent sector reporting,
- reliable chipset.

**Document your adapter:** model, chipset if known, and any quirks.

---

## Power and cabling

### Power stability
Low-level operations can stress a drive:
- higher write bursts,
- firmware transitions,
- internal GC spikes.

Ensure:
- adequate USB power (avoid weak ports),
- use externally powered enclosures if needed,
- short, high-quality cables.

### Cabling
- Use short USB cables.
- Avoid “charge-only” or thin cables.
- For microSATA, avoid flexing the connector.

---

## Optional but useful bench items

- ESD mat / wrist strap (protects small PCBs)
- A dedicated label system (drive ID, date, state)
- A small bench PSU for repeatable power testing
- IR thermometer or thermal probe (capture operating temperature)
- A “known good” reference SSD and adapter pair

---

## Camera-side considerations

- If you test with camera power, document:
  - camera model,
  - firmware version,
  - battery type / external power,
  - any additional modules in the chain.

Even when SATA identity reads work on data-only, real-world recording reliability should be tested with the full camera setup you intend to use.
---

⬅️ Prev: [SSD Guide](ssd-guide.md)  
➡️ Next: [REDMAG Validations Overview](redmag-validations-overview.md)

