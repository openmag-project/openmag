<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# Troubleshooting & Recovery

## MP tool does not detect the SSD

- Confirm the intended drive, administrator privileges, stable power, and correct controller/NAND package.
- Close CrystalDiskInfo, Disk Management, and other disk utilities.
- Try another direct USB port or an appropriate direct SATA connection.
- Check whether the bridge supports low-level commands; file-transfer support is insufficient.
- If normal detection still fails, consult the exact board's ROM/ISP procedure in the [Hardware Guide](03-hardware-guide.md).

---

## Programming ends in Fail

Capture the exact error and tool log before changing settings. Recheck NAND support, DRAM configuration, and the saved Auto/Default capacity mode. An incompatible NAND package is one cause, but not the only possible cause.

The PDF suggests trying another build for the **same supported controller/NAND combination**. It also notes that some recovery packages require **Download ISP** and the matching ISP binary. Use package-specific instructions; do not load an unrelated binary or change undocumented flash settings by trial and error.

---

## Drive no longer enumerates

A drive may still be detectable in documented ROM/ISP recovery mode. Some USB bridges fail to expose a controller in this state; direct SATA may help. Recovery is not guaranteed.

The PDF mentions an SPI programmer as a last resort. That is outside this guide's worked procedure and requires board-specific electrical and firmware knowledge. Do not assume every SSD has an accessible, recoverable external boot flash.

---

## Camera rejects media or will not format

Check the profile in order:

1. Model exactly `RED 480GB V1`.
2. Vendor `Red Digital `, including its trailing space, in the saved configuration.
3. Visible sector count exactly `937703088`, verified after full power removal.
4. Source's reported firmware `0308-000` and selected serial format.
5. Camera model/firmware and physical enclosure connections.

Serial and reported firmware are part of the source profile; their necessity is unconfirmed. Reprogramming may be needed for incorrect identity settings; capacity-only errors belong in the separate Linux HPA step. Capture evidence before making further changes.

---

## Camera accepts media but drops frames

Acceptance does not prove adequate sustained speed. Verify the workflow's physical DRAM requirement, then check post-cache write performance, temperature, power, and adapter/enclosure stability.

The PDF suggests a lower data rate (higher compression or lower resolution) as a diagnostic and a faster sustained-write SSD if performance remains inadequate. Do not attribute every dropped frame to missing DRAM. Retest long clips and inspect footage on a computer after any change.

---

## hdparm fails or capacity does not persist

- Re-identify the device by model and serial; its Linux name may have changed.
- Confirm administrator privileges (`sudo`), an unmounted target, and sufficient native capacity.
- If a USB bridge rejects the command, use an appropriate direct SATA connection.
- Check the exact error against drive/controller documentation; HPA support and locking behavior differ.
- Verify the first number in `hdparm -N` output, then verify again after full power removal.

The PDF suggests `hdparm -Y` followed by disconnecting a SATA data cable for a “frozen” drive. This port does **not** provide that as a general recovery instruction: sleep, ATA security state, and HPA locking are different issues, and live cable removal depends on host support. Use documented hardware-specific recovery instead.

---

Prev: [Working Example](working-example.md)  
Next: [Quick Reference](08-quick-reference.md)
