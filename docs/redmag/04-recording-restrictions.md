<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# Recording Restrictions

When a RED camera detects an SSD that does not fully pass validation:

- the media may still be detected
- formatting may succeed
- recording time is artificially limited

This behavior is intentional and designed to restrict the use of non-approved media.

## What “restricted recording” looks like

Depending on camera and firmware version, you may see:
- unexpectedly short record times
- warnings about media speed or compatibility
- recording that stops earlier than expected

## What fixes it

For REDMAG, tests indicate you must satisfy both:
1. a whitelisted model name, and
2. an exact capacity match between the model string and the drive’s reported capacity



---

[← REDMAG validation model](03-redmag-validation-model.md) | **Recording restrictions** | [High-level process →](05-high-level-process.md)
