![img](img/logo.png)
# uwuAOSP for POCO F7/REDMI Tubro 4 Pro (onyx)

**Installation and Update Guide**

This guide explains how to install uwuAOSP (Android 17) on the `onyx` , including clean installation and updating from a previous build.

> [!WARNING]
> **Flashing custom firmware involves risks.**
>
> - Back up all important data before proceeding.
> - Unlocking the bootloader and formatting data will erase user data.
> - Make sure your device is **POCO F7/REDMI Tubro 4 Pro (onyx)**.
> - Use only the images and ROM package provided for the same build.
> - Follow the instructions carefully. Incorrect flashing may result in boot failures or data loss.

## 1. Requirements

Before installation, make sure you have:

- A device that has already unlocked the bootloader
- Please prioritize using HyperOS firmware (OS3.0.305)
- A Windows, Linux, or macOS computer.
- The latest [Android SDK Platform-Tools](https://developer.android.com/tools/releases/platform-tools).
- A working USB cable.
- At least 50% battery charge.
- A complete backup of your important data.

**Google Apps (GApps) are already included.** Do not flash an additional GApps package unless explicitly instructed by the maintainer.

## 2. Download Required Files

Download the following files from the same build directory:

| File | Purpose |
|---|---|
| `uwuAOSP-version-date-onyx-sigined.zip` | ROM installation package |
| `boot.img` | Boot image |
| `dtbo.img` | Device Tree Overlay |
| `init_boot.img` | Init boot image |
| `vendor_boot.img` | Vendor boot image |
| `recovery.img` | Recovery image |

If you have already flashed other custom ROM before this, you can directly flash recovery.img and skip to continue here

**Important:** Never mix images from different builds unless the maintainer explicitly confirms compatibility.

## 3. Clean Installation

A clean installation is required when:

- Installing uwuAOSP for the first time.
- Switching from another custom ROM.
- Switching from another maintainer's uwuAOSP build.
- The maintainer explicitly requires a clean flash.

### Step 1 — Enter Fastboot Mode

1. Power off your device.
2. Hold **Volume Down + Power** until the FASTBOOT screen appears.
3. Connect your device to your computer using a USB cable.

Verify that your device is detected:

```bash
fastboot devices
```

Your device's serial number should appear.

### Step 2 — Flash Required Images

Open a terminal in the directory containing the downloaded files.

Execute the following commands, replacing `<date>` with your build date:

```bash
fastboot flash boot boot.img
fastboot flash dtbo dtbo.img
fastboot flash init_boot init_boot.img
fastboot flash vendor_boot vendor_boot.img
fastboot flash recovery recovery.img
```

Wait for each command to finish successfully before continuing.

**Do not reboot into the existing system at this stage.**

### Step 3 — Boot into Recovery

Reboot directly into recovery if your Fastboot implementation supports it:

```bash
fastboot reboot recovery
```

If the command is unsupported, use the device's hardware-key method to enter recovery.

1. Disconnect the USB cable if necessary.
2. Power off the device.
3. Hold **Volume Up + Power**.
4. Release the buttons when recovery starts.

> Recovery navigation depends on the recovery implementation. If touch input is unavailable, try using the volume buttons to navigate and the power button to confirm.

### Step 4 — Format Data

In Evolution X Recovery:

1. Select **Factory Reset**.
2. Select **Format data / factory reset**.
3. Confirm the operation.
4. Wait until formatting completes.

> [!CAUTION]
> **This step permanently erases user data, including files stored in internal storage.**
>
> Formatting data is required for a clean installation and may be necessary to initialize the data partition correctly.

### Step 5 — Install ROM
Return to the recovery main menu.

Select:

**Apply Update → Apply from ADB**

On your computer, execute:

```bash
adb sideload ROM_PACK.zip
```

Wait for the installation to finish.

> [!NOTE]
> The progress indicator on your computer may stop at approximately **47%**. This can be normal for ADB sideload.
>
> Check the recovery screen to confirm whether installation succeeded. Do not assume that every stop at 47% indicates success.

### Step 6 — Reboot

After installation completes successfully:

1. Return to the recovery main menu.
2. Select **Reboot system now**.
3. Wait for the device to boot.

The first boot may take longer than usual.

**Congratulations! uwuAOSP should now be installed.**

---

## 4. Updating from a Previous Build

If you are already running an earlier build maintained by the same developer, you may be able to update without formatting data.

> [!IMPORTANT]
> Local updates are supported only when the installed updater and build configuration allow them.
>
> Do not assume that builds from different maintainers are compatible with dirty flashing.
>
> Always follow any build-specific update instructions provided by the maintainer.

---

## 5. Verify File Integrity

If a `SHA256SUMS` file is provided, verify the downloaded files before flashing.

On Linux or macOS with compatible checksum utilities:

```bash
sha256sum -c SHA256SUMS
```

Run this command in the directory containing the downloaded files.

All required files should return `OK`.

If verification fails, download the affected file again.

Windows users can verify individual files using:

```powershell
Get-FileHash .\filename.zip -Algorithm SHA256
```

Compare the resulting hash with the value provided by the maintainer.

---

## 6. Troubleshooting

### Device not detected in Fastboot

- Check the USB cable and USB port.
- Install the appropriate USB drivers on Windows.
- Update Android SDK Platform-Tools.
- Try another USB port.

### ADB sideload fails

- Make sure the device is in **Apply from ADB** mode.
- Verify that the ZIP file is not corrupted.
- Confirm that the ROM package matches your device.
- Check the error message displayed in recovery.

### Device stuck on the boot animation

- Allow additional time for the first boot.
- Verify that the required firmware version is installed.
- Make sure all required images came from the same build.
- If coming from another ROM, confirm that a clean installation was performed.

If the problem persists, collect recovery logs or relevant error messages before requesting support.

---

## 7. Important Notes

- This is an **uwuAOSP build**.
- Only install packages intended for `onyx`.
- Do not relock the bootloader while running an unofficial custom ROM.
- Keep a backup of important data before updating.
- Report reproducible issues with logs and clear reproduction steps.

---

**Enjoy uwuAOSP on your device!**
