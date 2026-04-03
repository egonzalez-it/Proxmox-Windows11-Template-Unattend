# 🖥️ Proxmox Windows 11 Template Automation (Sysprep + Unattend)

![Windows](https://img.shields.io/badge/OS-Windows%2011-blue)
![Proxmox](https://img.shields.io/badge/Platform-Proxmox-orange)
![PowerShell](https://img.shields.io/badge/Automation-Unattend.xml-green)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

---

## 📌 Overview

This repository demonstrates a **lightweight and practical method** to automate Windows 11 virtual machine deployments in Proxmox using:

- **Sysprep (generalize + OOBE)**
- A custom **unattend.xml**
- Strategic placement of the unattend file in:
  ```
  C:\Windows\Panther\Unattend\
  ```

This approach allows cloned VMs from a Proxmox template to **automatically configure themselves on first boot**, without manual interaction.

---

## ⚠️ Important Disclaimer

> 🚫 **This method is NOT intended for production environments**

This solution is designed for:

- Lab environments
- Testing scenarios
- Rapid VM provisioning
- Learning and experimentation

It is **not recommended for enterprise deployments**, Autopilot, or standardized imaging pipelines due to:

- Lack of reliability guarantees
- Potential incompatibility with modern deployment tools
- Security concerns (e.g., plaintext credentials)

---

## 🎯 Purpose

The goal of this project is to:

- Simplify VM template creation in Proxmox
- Automate post-clone configuration
- Reduce manual OOBE steps
- Provide a reusable "gold image" workflow for labs

---

## 🧠 Why This Works

After running Sysprep with:

```
sysprep /generalize /oobe /shutdown
```

Windows enters the **OOBE (Out-of-Box Experience)** phase on next boot.

During this phase, Windows automatically searches for an unattend file in specific locations, including:

```
C:\Windows\Panther\
C:\Windows\Panther\Unattend\
```

By placing the file here **before Sysprep**, the unattend.xml is:

1. Preserved inside the image
2. Detected automatically on first boot
3. Applied during the OOBE phase

This allows the system to:

- Skip OOBE screens
- Create local users
- Apply registry tweaks
- Run first-logon commands

👉 This behavior is specific to **Sysprep-based deployments**, not ISO-based installations.

---

## 🔁 Workflow

### 1. Create Base VM in Proxmox
- Install Windows 11 normally

---

### 2. Enter Audit Mode
At OOBE screen:

```
Ctrl + Shift + F3
```

This logs you in as the built-in Administrator and bypasses OOBE.

---

### 3. Customize the Image

Install:
- Applications
- Updates
- Configurations

---

### 4. Add Unattend File

Create folder:

```
C:\Windows\Panther\Unattend\
```

Copy your `unattend.xml` into this directory.

---

### 5. Run Sysprep

Example:

```
sysprep /generalize /oobe /shutdown
```

---

### 6. Convert to Proxmox Template

- Mark VM as template
- Clone as needed

---

### 7. First Boot (Cloned VM)

On startup, Windows will:

- Detect unattend.xml
- Skip OOBE
- Apply configurations automatically

---

## ⚙️ What Can Be Automated

Using unattend.xml, you can:

- Skip OOBE screens
- Create local admin accounts
- Enable auto-logon
- Configure regional settings
- Apply registry tweaks
- Enable services (e.g., RDP)
- Run PowerShell commands at first logon

---

## ⚠️ Limitations

- Not suitable for Autopilot or Intune enrollment
- Panther folder behavior is not guaranteed across all scenarios
- May break after:
  - Windows feature updates
  - System resets
- Plaintext credentials pose security risks

---

## 👤 Author

Eduardo González  
L2 Technical Support | Microsoft 365 | Intune | Automation  

---

## 📄 License

MIT License
