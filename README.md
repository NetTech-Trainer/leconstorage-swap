# leconstorage
Here’s a clean, **Git-ready `README.md`** built from your command history.
You can copy-paste this directly into a Git repository.

---

# Swap Partition Setup on Linux (NVMe Disk)

This README documents the steps used to create and enable a **swap partition** on an NVMe disk using standard Linux tools.
The example device used here is `/dev/nvme0n2`.

---

## 📌 Prerequisites

* Root or sudo access
* Unused disk or free partition space
* Linux system (RHEL / CentOS / Rocky / Alma / Ubuntu)

---

## 🧱 Step 1: Partition the Disk

Use `fdisk` to create a partition on the target disk.

```bash
sudo fdisk /dev/nvme0n2
```

Inside `fdisk`, create a new partition and write changes.

---

## 🔍 Step 2: Verify Block Devices

List block devices to confirm the partition was created.

```bash
lsblk
```

---

## 🔁 Step 3: Create Swap Area

Format the partition as swap.

```bash
sudo mkswap /dev/nvme0n2p1
```

Expected output:

```
Setting up swapspace version 1
```

---

## 📄 Step 4: Verify Filesystem Type

Confirm the partition is now recognized as swap.

```bash
lsblk --fs
```

You should see the partition listed with type `swap`.

---

## ▶️ Step 5: Enable Swap

Activate the swap partition.

```bash
sudo swapon /dev/nvme0n2p1
```

---

## ✅ Step 6: Confirm Swap is Active

Recheck filesystem details and memory usage.

```bash
lsblk --fs
free -h
```

Example output:

* Swap shows as `[SWAP]`
* `free -h` displays total and used swap

---

## 🧠 Notes

* Swap helps prevent out-of-memory (OOM) conditions.
* On low-RAM systems, swap usage is normal.
* For persistence across reboots, add the swap UUID to `/etc/fstab`.

Example:

```text
UUID=<swap-uuid>   none   swap   sw   0   0
```

---

## 📎 Useful Commands

```bash
swapon --show
swapoff -a
blkid
```

---

## 🏁 Summary

✔ Disk partitioned
✔ Swap formatted
✔ Swap enabled
✔ System memory stabilized

This setup is suitable for **servers, VMs, and cloud instances**.

---
