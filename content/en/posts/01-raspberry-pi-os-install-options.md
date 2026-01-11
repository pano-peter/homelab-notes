---
title: "Installing Raspberry Pi OS – possibilities on different operating systems"
date: 2026-01-04
draft: false
---

You just got a Raspberry Pi, maybe for Christmas, or found an old one gathering dust.

The Raspberry Pi is a super popular single-board computer. Getting its operating system set up has gotten a lot easier lately. It's not just about burning an SD card anymore. Now you can create users, turn on SSH, set up networks, and even boot from USB or an M.2 SSD (for the Pi 5).

In this article, I'm not going to deep-dive into just one setup method. Instead, I'll cover all your options for installing Raspberry Pi OS across different operating systems like Windows, Linux, and macOS, and help you figure out which approach makes the most sense for you.

## The official way: Raspberry Pi Imager

![Raspberry Pi Imager OS selection]( /homelab-notes/images/en/imager_01_en.png )

### Why did we need the Raspberry Pi Imager?

Back in the early days of Raspberry Pi, there wasn't a single official tool for installation. Installing Raspberry Pi OS (which was called Raspbian back then) meant manually downloading an image, using separate programs like `dd` or Win32 Disk Imager, and you absolutely needed a monitor and keyboard for the first boot. The system always started with the default `pi` / `raspberry` user.

Running it headless (without a monitor or keyboard) became possible later through unofficial or undocumented tricks, like an empty `ssh` file or a manually created `wpa_supplicant.conf`. These worked, but they weren't easy for beginners and it was easy to mess things up.

The Raspberry Pi Imager came along to replace that scattered process with one easy-to-use graphical tool. Its main goal was to make installing the OS much friendlier, without losing the ability to do advanced setups.

Now, the Raspberry Pi Imager, made by the Raspberry Pi Foundation, is pretty much the go-to tool for installing Raspberry Pi OS.

### What can the Raspberry Pi Imager do?

- Download Raspberry Pi OS (and other operating systems)
- Write the image to an SD card or USB drive
- **Pre-configure settings like**:
  - Username and password
  - **Enable SSH**
  - Device hostname
  - Wi-Fi settings
  - Location (time zone, keyboard layout)
  - Raspberry Pi Connect setup

It's recommended to set up your user, a strong password, and enable SSH with key-based authentication (if you'll access the Pi remotely) right from here. That way, after the first boot, your system is pretty much ready to go.

If you don't need a graphical interface or desktop apps, picking Raspberry Pi OS Lite is good idea. It uses fewer computer resources, boots faster, and has a smaller attack surface.

### What operating systems is it available on?

- **Windows**
- **macOS** (Intel and Apple Silicon)
- **Linux** (AppImage, package manager, or Flatpak)

### Advantages and bad points

**Advantages:**
- Easy for beginners
- Fast
- Fewer mistakes

**Disadvantages:**
- Less control over what's happening behind the scenes
- Limited for automating tasks

---

## Installing Raspberry Pi OS on Linux, without the Imager

Many Linux users still prefer the classic, manual methods.

### Basic steps:

1. Download the Raspberry Pi OS image (ZIP or XZ)
2. Unzip it
3. Write it to an SD card or USB device, for example, using 'dd'

This method works on any Linux distribution, but you need to be careful, especially **when picking the right drive**.

### Headless setup with files

You can pre-configure the system using files placed on the boot partition, or in more advanced cases, by changing files on the system partition:

- `ssh` – to enable SSH
- `userconf` / `userconf.txt` – to create a user
- `wpa_supplicant.conf` – for Wi-Fi settings
- Add SSH keys
- Set `config.txt`

This solution is great for scripting, making it perfect for **automated setups**.

### Advantages and disadvantages

**Advantages:**
- Complete control
- Easy to integrate into CI / provisioning

**Disadvantages:**
- Easy to make mistakes
- More manual steps

---

## Installing on Windows

On Windows, the Raspberry Pi Imager is pretty much essential.

### Tools you can use:

- Raspberry Pi Imager (recommended)
- Balena Etcher
- Win32 Disk Imager (more for older systems)

### Common problems:

- Picking the wrong drive
- Permission issues
- Antivirus interfering during image writing

---

## Installing on macOS

On macOS, the Imager is also the easiest way, but using command-line tools is also popular.

### Command-line tools:

- `diskutil` – to find drives
- `dd` – to write the image

### Common pitfalls:

- Drives automatically mounting while writing
- Permission requests to access the device

---

## Special situations

**Raspberry Pi OS Lite versus Desktop**
The Desktop version includes a graphical interface and pre-installed apps, which is nice for learning or general desktop use. But if your Pi is a server, runs a service, or is an embedded device, the Lite version is better. It uses fewer resources, starts faster, and has a smaller attack surface.

**Boot from USB drive**
Starting with the Pi 4, you can boot from USB drives (like flash drives or SSDs). USB storage is generally faster and more reliable than a microSD card, especially for continuous use or tasks that involve a lot of data, like a database.

---

## Which method should you pick?

- **Beginner user**: Raspberry Pi Imager
- **Headless server**: Imager or manual Linux method
- **Multiple Pis, automation**: Manual image setup + scripting

---

## Summary

There are now many ways to install Raspberry Pi OS, and there isn't one perfect method for everyone. The new Raspberry Pi Imager solves a lot of old headaches, but in a Linux environment, there's still a place for manual, scriptable approaches.
