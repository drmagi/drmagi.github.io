---
title: "Which Hardware is it?"
description: "How to find out which components are in a computer. Created with AI support."
categories: [Hardware]
---

Finding out what hardware components are inside your computer is straightforward on both Windows and Linux. Depending on whether you prefer a graphical user interface (GUI) or the command line, here are the most effective ways to check your CPU, RAM, storage (SSD/HDD), and GPU.


## In Windows

### Method 1: Task Manager (Fastest GUI for Basics)

1. Press **Ctrl + Shift + Esc** to open the **Task Manager**.
2. Click on the **Performance** tab (the speedometer icon on the left or top).
3. Here you can click through each category:
* **CPU:** Shows processor model, core count, and speed.
* **Memory:** Shows total RAM size, speed, and slots used.
* **Disk (C:, etc.):** Shows whether your drive is an SSD or HDD and its total capacity.
* **GPU:** Shows your graphics card model and dedicated memory.


### Method 2: System Information (`msinfo32`)

1. Press **Win + R** to open the Run dialog box.
2. Type `msinfo32` and press **Enter**.
3. The **System Summary** window will open, displaying your exact Windows version, motherboard model ("BaseBoard Manufacturer/Product"), processor, and total installed RAM.

### Method 3: PowerShell (For Detailed Specifications)

If you want precise technical part numbers and speeds via the command line:

1. Right-click the Start button and select **Terminal** or **PowerShell**.
2. Run the following commands:
* **For CPU:** `Get-CimInstance Win32_Processor | Select-Object Name, MaxClockSpeed, NumberOfCores`
* **For RAM:** `Get-CimInstance Win32_PhysicalMemory | Select-Object Manufacturer, Capacity, Speed, PartNumber`
* **For Storage:** `Get-PhysicalDisk | Select-Object DeviceId, FriendlyName, MediaType, Size`


## In Linux

Linux provides powerful command-line utilities to inspect every detail of your hardware.

### Method 1: Quick Individual Commands

* **CPU Information:** Run `lscpu` to see processor architecture, model name, cores, and clock speeds.
* **RAM Usage & Size:** Run `free -h` for total and available memory, or `lshw -C memory` for detailed stick-by-stick information. Additionally, you can use `dmidecode` as a powerful command-line tool used to dump a computer's DMI (Desktop Management Interface) table — sometimes called the SMBIOS table — into a human-readable format. It reads what the motherboard's BIOS/UEFI firmware reports about the physical hardware components. 
```bash 
sudo dmidecode
```
* **Storage (SSD/HDD):** Run `lsblk` to list all block devices (drives and partitions) along with their types and sizes. You can check if a drive is an SSD or HDD by running `cat /sys/block/sda/queue/rotational` (if it returns `0`, it's an SSD; `1` means a mechanical HDD).

### Method 2: `inxi` (Best All-in-One Summary)

`inxi` is a fantastic tool that outputs a clean, color-coded summary of your entire system.

1. Install it if it isn't already (e.g., `sudo apt install inxi` on Ubuntu/Debian or `sudo dnf install inxi` on Fedora).
2. Run the full system report:
```bash
inxi -Fz

```

*(The `-F` flag gives a full report, and `-z` hides sensitive data like your IP address).*

### Method 3: `lshw` (List Hardware)

To generate a comprehensive list of all components categorized by hardware type:

```bash
sudo lshw -short

```

*Note: You can target specific hardware classes using flags like `sudo lshw -C cpu`, `sudo lshw -C disk`, or `sudo lshw -C memory`.*