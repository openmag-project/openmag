<p align="center">
  <img src="../../assets/logo.jpg" alt="openMAG logo" />
</p>

# Linux Sector Count Guide

## Goal and preconditions

After MP programming, set the test SSD to **937,703,088 visible 512-byte sectors** using Linux `hdparm`. This is separate from partitioning or camera formatting.

**This operation changes persistent drive capacity and can make data inaccessible.** Use an expendable SSD with no needed data. Disconnect unrelated drives where practical, identify the target by model and serial, and unmount all its partitions. These commands are documentation examples; `/dev/sdX` must be replaced with the confirmed whole-drive device, never a partition such as `/dev/sda1`.

---

## Part A: Prepare a live USB

Skip to Part C if you already have a suitable Linux host.

1. Download an [Ubuntu Desktop ISO](https://ubuntu.com/download/desktop) and [Rufus](https://rufus.ie/) or [balenaEtcher](https://etcher.balena.io/).
2. Insert a spare USB stick of at least 8GB, with enough space for the chosen ISO. Creating the installer erases the stick.
3. In Rufus, select that USB device and the ISO. The source uses GPT/UEFI and ISO mode; use settings appropriate to your host and the selected image rather than forcing a filesystem the tool does not offer.
4. Confirm the selected USB device, start writing, and wait for **Ready**.

---

## Part B: Boot without installing

1. Connect the programmed test SSD and bootable USB.
2. Restart and open your computer's boot-device menu. The source gives examples such as ASRock/MSI F11, ASUS F8, Gigabyte/Dell/Lenovo F12, and HP F9; consult the host's instructions because keys vary by model.
3. Choose the USB's UEFI boot entry where appropriate.
4. Select **Try Ubuntu**, rather than installing over an existing system.
5. Open Terminal, for example with Ctrl+Alt+T. Ensure `hdparm` is available (`hdparm -V`); if missing, install it through the distribution's package manager before continuing.

---

## Part C: Identify and inspect the target

```sh
lsblk -o NAME,MODEL,SERIAL,SIZE,LOG-SEC,MOUNTPOINTS
sudo hdparm -I /dev/sdX
sudo hdparm -N /dev/sdX
```

Confirm the model and serial match your programmed SSD. **Do not select a drive by approximate size or drive letter alone**: device names can change and multiple drives may be similar sizes. Confirm the logical sector size is 512 bytes and the native count is at least `937703088`. If either condition fails, stop; this profile does not cover that device.

Before modification, unmount any mounted target partitions using the desktop's unmount control or `umount` with each confirmed partition path. Do not change the capacity of a mounted filesystem or the host's system disk.

---

## Part D: Set the persistent visible count

Only after confirming the target, run:

```sh
sudo hdparm -N p937703088 --yes-i-know-what-i-am-doing /dev/sdX
```

Here `-N` changes the visible count, `p` requests a persistent setting, and `/dev/sdX` identifies the whole SSD. The [hdparm manual](https://man7.org/linux/man-pages/man8/hdparm.8.html) warns that changing this limit risks data loss. Persistence and command support depend on the drive and connection; an error is not success.

Read back the result:

```sh
sudo hdparm -N /dev/sdX
```

The first value in the visible/native pair must be `937703088`. If the second is larger, the remaining sectors are hidden by HPA. Do not rely on the PDF's sample “HPA is disabled” label when interpreting unequal values.

---

## Part E: Verify persistence

1. Shut down Linux and fully power off/disconnect the test SSD.
2. Reconnect, identify its current device name again, and repeat the read-only checks in Part C.
3. Confirm the visible count remains `937703088`, with 512-byte logical sectors.
4. Save the output in your test notes, shut down, and remove the USB/SSD for camera testing.

If the bridge rejects HPA commands, try a suitable direct SATA connection. If the device is locked or reports a frozen condition, capture the exact error and consult controller-specific documentation; do not apply a generic cable-disconnection remedy. See [Troubleshooting & Recovery](07-troubleshooting-and-recovery.md).

---

Prev: [MP Tool Guide](05-mp-tool-guide.md)  
Next: [Working Example](working-example.md)
