
## 🧩 STEP 1: Install Timeshift

On Arch:

```bash
sudo pacman -S timeshift
```

---

## 🧩 STEP 2: Enable Btrfs Snapshots in Timeshift

Run the setup:

```bash
sudo timeshift --create --btrfs
```

Then launch the GUI or TUI:

```bash
sudo timeshift-gtk
```

### ➕ Setup:
- **Snapshot Type**: `BTRFS`
- **Snapshot Location**: your root (`/`) subvolume (should auto-detect)
- Set it to **manual** or **boot** snapshot (based on your use)
- Make one initial snapshot called `"Clean Install"` (we'll mark it special later)

---

## 🧩 STEP 3: Verify Subvolume Structure

Make sure Timeshift is using its own subvolume:

```bash
sudo btrfs subvolume list /
```

You should see something like:

```
ID 256 gen ... path <root>
ID 257 gen ... path timeshift-btrfs/snapshots
```

If Timeshift is installed properly, it will auto-create its own subvolume at `/timeshift-btrfs`.

---

## 🧩 STEP 4: Add Timeshift to GRUB Boot Menu

Timeshift includes a script to do this!

### 🛠️ Install the boot integration hook:
```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

If you already have snapshots, Timeshift will auto-detect them and inject them into the bootloader.

You can also force it with:
```bash
sudo timeshift --grub
```

> This adds entries like:
> `Timeshift: Snapshot 2025-04-21_15-30-00`

Now, on boot, GRUB will list your snapshots. You can boot into one just like a regular OS option.

---

## 🧩 STEP 5: Restore Snapshot from GRUB (When Needed)

1. Boot your system
2. Select a snapshot entry under `Timeshift` in the GRUB menu
3. It boots into that snapshot (readonly)
4. From there, you can:
   - Use Timeshift to **restore it permanently**
   - Mount and copy back configs manually if needed

---

## 🧩 STEP 6 (Optional): Automate Snapshot on Boot or Weekly

In Timeshift GUI:
- Go to `Settings` → `Schedule`
- Enable **Boot** or **Weekly** snapshots

You can also automate via systemd timers if you want finer control.

---

## ✅ Summary

| Step              | What it does                           |
| ----------------- | -------------------------------------- |
| Install Timeshift | Enables snapshot creation on Btrfs     |
| Setup Snapshots   | Create initial snapshot after setup    |
| GRUB Hook         | Adds snapshots to GRUB boot menu       |
| Boot Restore      | Lets you recover system via GRUB entry |
