# Xiaomi AX3200 & Redmi AX6S Firmware Installation Guide

## Overview

The **Xiaomi AX3200 (Model RB01, International Version)** and **Redmi AX6S (Model RB03, Chinese Version)** share identical hardware specifications. The only difference between the two is the version of the stock firmware, which is region-locked.

### Important Note

- **Device Models**:
  - **Xiaomi AX3200 (RB01)**
  - **Redmi AX6S (RB03)**

Both versions utilize the same hardware.

## Purpose

The primary goal of removing the stock firmware and installing **OpenWRT** is to take advantage of its open-source nature, which offers several benefits:

- **Lightweight**: OpenWRT is a more efficient firmware compared to the stock version, providing better performance on your device.
- **Freedom and Control**: OpenWRT grants users greater freedom to customize their router settings and configurations.
- **Enhanced Security**: With OpenWRT, you can implement advanced security features, including the ability to hide your real MAC address and other privacy enhancements.

## Prerequisites

Before proceeding, ensure that your device has Telnet enabled. If Telnet is not enabled, you will need to run a Python script to gain root access.

### Required Tool

- **[Xiaomi Router Patcher](https://github.com/c0m1-dev/XiaomiRouterPatcher.git)**: This script is essential for enabling Telnet access on your router.

### Connection Requirement

- Ensure you are connected to the router via **Ethernet cable**.

## Steps to Enable Telnet Access

1. **Download the Xiaomi Router Patcher**:
   ```bash
   git clone https://github.com/c0m1-dev/XiaomiRouterPatcher.git
   cd XiaomiRouterPatcher

Run the Python Script to gain root access.

## Connecting to the Router
After enabling Telnet, follow these steps to connect using WinSCP.

## WinSCP Setup
Open WinSCP and configure the connection settings:

File Protocol: SCP
Hostname: 192.168.31.1
SSH Port: 22 (leave as default)
Username: root
Password: root (or your chosen password)
Login to the router.

## Uploading OpenWRT Firmware

Once connected, navigate to the /tmp folder.
Drag and drop the OpenWRT firmware file: openwrt-23.05.3-mediatek-mt7622-xiaomi_redmi-router-ax6s-squashfs-factory.bin
Save and close WinSCP.

## Connecting via PuTTY
Download and Install PuTTY from putty.org.

Open PuTTY and enter the following:

Host Name (or IP address): 192.168.31.1
Port: 22 (leave as default)
Click Open and log in with root access.

## Running Commands
Once logged in, execute the following commands:

For 2022 Bootloader:

nvram set ssh_en=1
nvram set uart_en=1
nvram set boot_wait=on
nvram set flag_boot_success=1
nvram set flag_try_sys1_failed=0
nvram set flag_try_sys2_failed=0
nvram commit
cd /tmp
mtd -r write openwrt-23.05.3-mediatek-mt7622-xiaomi_redmi-router-ax6s-squashfs-factory.bin firmware
nvram set flag_ota_reboot=1
nvram commit
reboot

## For New Bootloader:

nvram set boot_fw1="run boot_rd_img;bootm"
nvram set flag_try_sys1_failed=8
nvram set flag_try_sys2_failed=8
nvram set flag_boot_rootfs=0
nvram set flag_boot_success=1
nvram set flag_last_success=1
nvram commit
cd /tmp
mtd -r write openwrt-23.05.3-mediatek-mt7622-xiaomi_redmi-router-ax6s-squashfs-factory.bin firmware
nvram set flag_ota_reboot=1
nvram commit
reboot

## Accessing the Router
After the router reboots, you can access it via:

IP Address: 192.168.1.1

