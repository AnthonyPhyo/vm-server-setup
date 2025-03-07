# Windows Server 2025 Setup on VirtualBox

## Table of Contents
1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Creating a Virtual Machine](#creating-a-virtual-machine)
4. [Installing Windows Server 2025](#installing-windows-server-2025)
5. [Post-Installation Setup](#post-installation-setup)
6. [Installing VirtualBox Guest Additions](#installing-virtualbox-guest-additions)
7. [Optional Configurations](#optional-configurations)
8. [Troubleshooting](#troubleshooting)
9. [Additional Resources](#additional-resources)

---

## Introduction
This guide provides step-by-step instructions on how to install and configure **Windows Server 2025** on **VirtualBox** for testing and development purposes.

## Prerequisites
- **VirtualBox** installed ([Download Here](https://www.virtualbox.org/))
- **Windows Server 2025 ISO** (from Microsoft Insider Preview)
- At least **8GB RAM**, **60GB disk space**, and **VT-x/AMD-V enabled** in BIOS
- Internet connection for updates

## Creating a Virtual Machine
1. Open **VirtualBox** and click **"New"**.
2. Set:
   - **Name**: Windows Server 2025
   - **Type**: Microsoft Windows
   - **Version**: Windows 2022 (64-bit)
3. Allocate resources:
   - **RAM**: Minimum **4GB or 4096MB** (recommended **8GB+**)
   - **CPUs**: At least **2** (recommended **4**)
4. Create a **Virtual Hard Disk**:
   - Choose **Create a Virtual Hard Disk Now**
   - Select **Pre-allocate Full Size**
   - Set disk size to **60GB or more**

## Installing Windows Server 2025
1. Go to **Settings → Storage**
2. Under **Devices**, select **Empty**
3. Click the **CD icon on the right under "Attributes"** → Choose **"Choose a disk file"**
4. Select the **Windows Server 2025 ISO**
5. Start the VM and boot from the ISO
6. Follow the Windows installation steps:
   - Select **Language, Time, and Keyboard Layout** → Click **Next**
   - Choose **Install Windows Server** and click **Next**
   - Choose **Windows Server 2025 Standard/Datacenter** (I did Datacenter Evaluation(Desktop Experience)
   - Select **Custom Installation** → Choose your virtual disk → Click **Next**
7. Wait for installation and restart when prompted

## Post-Installation Setup
- Set a **secure Administrator password**
- Log in and configure basic settings
- Set a **static IP** if needed
- Enable **Remote Desktop Access** (`System Properties > Remote Settings`)

## Installing VirtualBox Guest Additions
1. Click **Devices** in VirtualBox
2. Select **Insert Guest Additions CD Image**
3. Open **File Explorer → This PC → VirtualBox Guest Additions CD**
4. Run `VBoxWindowsAdditions.exe`
5. Restart the VM

## Optional Configurations
### 1. Installing Server Roles
Install Active Directory:
```powershell
Install-WindowsFeature -Name AD-Domain-Services -IncludeManagementTools
```
Install DHCP & DNS:
```powershell
Install-WindowsFeature -Name DHCP -IncludeManagementTools
Install-WindowsFeature -Name DNS -IncludeManagementTools
```
Enable IIS Web Server:
```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## Troubleshooting
| Issue | Solution |
|--------|------------|
| VirtualBox driver error | Run `sc.exe query vboxsup` and restart VirtualBox |
| No internet access | Use Bridged Adapter instead of NAT |
| Remote Desktop not working | Enable in `System Properties > Remote Settings` |

## Additional Resources
- [Windows Server Documentation](https://learn.microsoft.com/en-us/windows-server/)
- [VirtualBox Official Guide](https://www.virtualbox.org/wiki/Documentation)

---

### Author: Your Name
Last Updated: `YYYY-MM-DD`
