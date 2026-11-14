<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# Capacity Overview

## Exact target

The source specifies **937,703,088 visible sectors** for the `RED 480GB V1` profile, with 512-byte logical sectors:

```text
937703088 × 512 = 480103981056 bytes
                  ≈ 480.104 GB (decimal)
                  ≈ 447.132 GiB (binary)
```

A camera display near **447.1 GiB** is consistent with this target but does not prove the exact sector count. Record the device's numerical report.

---

## MP tool capacity versus Linux capacity

For this MINIMAG procedure the source says:

- **Disk Size: Auto**.
- Select **Default**, not IDEMA.
- Leave **Setting Capacity manually unchecked**.
- Program first, then use Linux `hdparm` to set the visible count.

This differs from the REDMAG MP Tool Guide's IDEMA selection. Do not copy that REDMAG setting into this profile. The PDF reports that manual sector-count configuration inside the MP tool can cause programming failure.

---

## Host Protected Area (HPA)

HPA limits the capacity exposed to the host. The SSD must already have at least the target native capacity; reducing the visible size cannot make a smaller drive larger. A partition resize or filesystem format does not set the drive's ATA visible sector count.

The Linux [hdparm manual](https://man7.org/linux/man-pages/man8/hdparm.8.html) defines `-N` as the visible sector count setting; `p` requests persistence. Its report gives visible/native counts. When visible is below native, the difference is hidden by an **enabled** HPA. The PDF's sample labels that case “disabled”; compare the numerical values instead.

Changing this limit can make existing data inaccessible. Follow the [Linux Sector Count Guide](06-linux-sector-count-guide.md) on an expendable, unmounted drive and verify again after a full power cycle.

---

Prev: [Whitelist Overview](04a-whitelist-overview.md)  
Next: [MP Tool Guide](05-mp-tool-guide.md)
