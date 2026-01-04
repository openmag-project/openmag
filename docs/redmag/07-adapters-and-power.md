<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# Adapters, Power, and External Testing

Most REDMAG instability reports trace back to **power** or **adapters**.

## The core rule

- The camera expects a SATA device on its data interface.
- The SSD must receive the **correct voltage** and sufficient current under sustained write load.

## External power setups (why they help)

External power can:
- reduce load on camera power rails
- allow use of 5V-only SSDs (2.5" SATA)
- make bench testing safer and more repeatable

## External testing flow (safe)

1. Verify the SSD enumerates reliably on a computer with your chosen adapter/cable.
2. Stress test the SSD on the computer (sustained write) to ensure it does not drop out.
3. Only then connect the SATA data path to the camera interface.
4. Run the camera validation sequence from the workflow page.

## Grounding and stability

If the SSD is externally powered but data is connected to the camera, ensure:
- common ground between the power supply and camera/data path
- stable connectors (no loose SATA cables)
- strain relief to prevent intermittent disconnects

> Placeholder: wiring diagrams and recommended bench-testing setups.



---

[← MP Tools overview](06-mp-tools-overview.md) | **Adapters and power** | [Gotchas and troubleshooting →](08-known-gotchas.md)
