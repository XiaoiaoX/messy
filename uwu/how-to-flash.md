
<p align="center">
  <img src="img/logo.png" width="800" alt="uwuAOSP Logo">
</p>

<h1 align="center">uwuAOSP for POCO F7 / Redmi Turbo 4 Pro (onyx)</h1>

<p align="center">
  <b>Android 17 | Installation & Update Guide</b>
</p>

<p align="center">
  <a href="#1-requirements">Requirements</a> •
  <a href="#2-download-required-files">Downloads</a> •
  <a href="#3-clean-installation">Installation</a> •
  <a href="#4-updating-from-a-previous-build">Updates</a> •
  <a href="#6-troubleshooting">Troubleshooting</a>
</p>

---

## Introduction

This guide explains how to install uwuAOSP (Android 17) on the POCO F7 and Redmi Turbo 4 Pro (`onyx`), including clean installation and updating from a previous build.

> [!WARNING]
> **Flashing custom firmware involves risks.**
>
> - Back up all important data before proceeding.
> - Unlocking the bootloader and formatting data will erase user data.
> - Make sure your device is **POCO F7 / Redmi Turbo 4 Pro (onyx)**.
> - Use only images and ROM packages provided for the same build.
> - Incorrect flashing may result in boot failures or data loss.
> - Proceed at your own risk.

---

## 1. Requirements

Before installation, make sure you have:

- A POCO F7 or Redmi Turbo 4 Pro (`onyx`) with an unlocked bootloader.
- **HyperOS firmware OS3.0.305** (recommended).
- A Windows, Linux, or macOS computer.
- The latest [Android SDK Platform-Tools](https://developer.android.com/tools/releases/platform-tools).
- A working USB cable.
- At least 50% battery charge.
- A complete backup of your important data.

> [!NOTE]
> **Google Mobile Services (GMS) are already included.**
>
> You do not need to install a separate GApps package.

---

## 2. Download Required Files

Download all required files from the same build directory.

| File | Description |
|---|---|
| `uwuAOSP-version-date-onyx-signed.zip` | ROM installation package |
| `boot.img` | Boot image |
| `dtbo.img` | Device Tree Overlay |
| `init_boot.img` | Init boot image |
| `vendor_boot.img` | Vendor boot image |
| `recovery.img` | Recovery image |

> [!IMPORTANT]
> - Use only files from the same build.
> - Do not mix images from different ROMs or releases.
> - Replace the example ROM ZIP filename with the actual downloaded filename.
> - Flash all required images unless the maintainer explicitly provides alternative instructions.

---

## 3. Clean Installation

A clean installation is required when:

- Installing uwuAOSP for the first time.
- Switching from another custom ROM.
- Switching from another maintainer's build.
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

If no device is detected, check your USB connection and drivers before proceeding.

### Step 2 — Flash Required Images

Open a terminal in the directory containing the downloaded images.

Execute the following commands:

```bash
fastboot flash boot boot.img
fastboot flash dtbo dtbo.img
fastboot flash init_boot init_boot.img
fastboot flash vendor_boot vendor_boot.img
fastboot flash recovery recovery.img
```

Wait for each command to complete successfully before continuing.

> [!IMPORTANT]
> Do not reboot into the existing system at this stage.
>
> If any flashing command fails, stop and investigate the error before proceeding.

### Step 3 — Boot into Recovery

After flashing the required images, reboot into recovery.

If supported by your Fastboot implementation:

```bash
fastboot reboot recovery
```

If this command is unsupported, use the hardware buttons to enter recovery:

1. Power off the device.
2. Hold **Volume Up + Power**.
3. Release the buttons when recovery starts.

> [!NOTE]
> Recovery navigation depends on the recovery implementation.
>
> If touch input is unavailable, try using the volume buttons to navigate and the power button to confirm.

### Step 4 — Format Data

In the recovery menu:

1. Select **Factory Reset**.
2. Select **Format data / factory reset**.
3. Confirm the operation.
4. Wait until formatting completes.

> [!CAUTION]
> **This operation permanently erases user data.**
>
> All installed apps, settings, and files stored in internal storage will be deleted.
>
> Make sure you have backed up your important data before continuing.

Formatting data is required for a clean installation.

### Step 5 — Install uwuAOSP

Return to the recovery main menu.

Select:

**Apply Update → Apply from ADB**

On your computer, execute:

```bash
adb sideload ROM_PACK.zip
```

Replace `ROM_PACK.zip` with the actual filename of your downloaded uwuAOSP package.

For example:

```bash
adb sideload uwuAOSP-version-date-onyx-signed.zip
```

Wait for the installation to complete.

> [!NOTE]
> The ADB sideload progress indicator on your computer may stop at approximately **47%**.
>
> This can be normal behavior.
>
> Always check the recovery screen to confirm that installation completed successfully.

### Step 6 — Reboot to System

After installation completes successfully:

1. Return to the recovery main menu.
2. Select **Reboot system now**.
3. Wait for the device to boot.

The first boot may take longer than usual.

**Congratulations! uwuAOSP is now installed on your device!**

---

## 4. Updating from a Previous Build

If you are already running an earlier uwuAOSP build maintained by the same developer, you may be able to update without formatting user data.

### Before Updating

- Back up your important data.
- Download the latest compatible uwuAOSP package.
- Read the changelog for build-specific instructions.
- Make sure the update is intended for your device.

### Local Update

If your installed build supports local updates:

1. Open **Settings → System → Updater**.
2. Select **Local Update**.
3. Choose the downloaded ROM ZIP.
4. Follow the on-screen instructions.
5. Reboot when prompted.

> [!IMPORTANT]
> Local updates require a compatible updater and build configuration.
>
> Do not assume that builds from different maintainers support dirty flashing.
>
> If local updating is unavailable, follow the update instructions provided with the release.
>
> Do not format data during a supported dirty-flash update unless explicitly instructed.

---

## 5. Verify File Integrity

If a `SHA256SUMS` file is provided, verify the downloaded files before flashing.

### Linux

Run:

```bash
sha256sum -c SHA256SUMS
```

All verified files should return `OK`.

### macOS

Use a compatible `sha256sum` utility, or calculate an individual file hash with:

```bash
shasum -a 256 ROM_PACK.zip
```

### Windows

Open PowerShell and run:

```powershell
Get-FileHash .\ROM_PACK.zip -Algorithm SHA256
```

Compare the resulting hash with the checksum provided by the maintainer.

> [!WARNING]
> If checksum verification fails, do not flash the affected file.
>
> Download it again and repeat verification.

---

## 6. Troubleshooting

### Device Not Detected in Fastboot

If `fastboot devices` returns no device:

- Check your USB cable and USB port.
- Install the appropriate USB drivers on Windows.
- Update Android SDK Platform-Tools.
- Try another USB port.
- Confirm that the device is in Fastboot mode.

### ADB Sideload Fails

If the installation fails:

- Make sure the device is in **Apply from ADB** mode.
- Verify that the ROM ZIP is not corrupted.
- Confirm that the package is intended for `onyx`.
- Check the error message displayed in recovery.
- Make sure the required images were flashed successfully.

### Device Stuck on Boot Animation

If the device does not finish booting:

- Allow additional time for the first boot.
- Verify that the recommended firmware is installed.
- Confirm that all flashed images came from the same build.
- If switching from another ROM, make sure a clean installation was performed.

If the problem persists, collect recovery logs or relevant error messages before requesting support.

### Recovery Does Not Boot

If recovery fails to start:

- Confirm that the correct recovery image was used.
- Check whether all required images were flashed successfully.
- Verify that the images belong to the same build.
- Review any Fastboot errors.

Do not flash unrelated recovery images without confirming compatibility.

---

## 7. Important Notes

- This guide is intended for **uwuAOSP on POCO F7 / Redmi Turbo 4 Pro (onyx)**.
- Only install packages specifically built for `onyx`.
- Do not relock the bootloader while running an unsupported custom ROM.
- Keep a backup of important data before installing updates.
- Report reproducible issues with logs and clear reproduction steps.

---

## Credits

Special thanks to **AdarshGrewal** & all onyx maintainers for their contributions and support.

---

<p align="center">
  <b>Enjoy uwuAOSP on your device!</b>
</p>

<p align="center">
  Made with ❤️ for the Android community.
</p>

<p align="center">
  <b>Powered by xiaoiaox</b>
</p>
