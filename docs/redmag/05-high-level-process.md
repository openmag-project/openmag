<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# High-Level Process

This page describes the full workflow at a high level, with practical preparation and validation steps.
Certain low-level modification steps can permanently damage hardware, so this guide focuses on
**safe, repeatable, and verifiable** phases.

## Phase 1: Establish a baseline (required)

1. Keep one known-good REDMAG unchanged.
2. Confirm the camera behaves normally with the baseline media:
   - detect media
   - format
   - record a short clip
   - offload and verify playback
3. Write down:
   - camera model and firmware version
   - baseline REDMAG model string (as shown by the camera or host system)

## Phase 2: Choose your experimental SSD

1. Prefer mSATA when possible (see the hardware page).
2. Record the SSD’s current identity and capacity before any changes.
3. Confirm the SSD is healthy (SMART health / attributes where available).

## Phase 3: Prepare your test setup

You will want a repeatable setup that reduces risk to your camera:

- Use external power where possible (see Adapters and Power).
- Keep a consistent SATA data path (avoid swapping unknown adapters mid-test).
- Capture logs and photos so results can be reproduced.

## Phase 4: Apply changes (advanced, high risk)

Some users modify SSD identity/capacity using manufacturer provisioning tooling.
This can brick SSDs when misconfigured.

This project documents concepts, risks, and compatibility findings, and encourages
safe, legal, and responsible experimentation.

## Phase 5: Validate in-camera (required)

After any change, validate with the same sequence every time:

1. Insert media and confirm detect
2. Format in-camera
3. Record a short clip
4. Record a longer clip (stress test)
5. Offload the clips
6. Verify integrity (checksum compare if possible)

> Placeholder: validation checklist screenshot and example run log



---

[← Recording restrictions](04-recording-restrictions.md) | **High-level process** | [MP Tools overview →](06-mp-tools-overview.md)
