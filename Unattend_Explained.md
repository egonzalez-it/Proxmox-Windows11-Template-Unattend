# Unattend.xml -- Detailed Overview and Customization Guide

## 📌 Purpose

This `unattend.xml` file is designed to automate the Windows 11 setup
process, specifically for lab environments and Proxmox VM template
deployments.

It allows you to skip manual configuration steps and deploy
preconfigured systems quickly.

------------------------------------------------------------------------

## ⚙️ What This File Actually Does

### 1. 🚀 Bypasses OOBE (Out-of-Box Experience)

-   Skips Microsoft account setup
-   Skips network configuration
-   Skips EULA and privacy prompts

Result: The system boots directly to the desktop without user
interaction.

------------------------------------------------------------------------

### 2. 🌎 Sets Language and Regional Settings

-   Language: English (US)
-   Input: US keyboard
-   Timezone: Eastern Standard Time

You can modify this depending on your location.

------------------------------------------------------------------------

### 3. 👤 Creates a Local Administrator Account

-   Username: `ladmin`
-   Password: `Pa$$w0rd`
-   Group: Administrators

⚠️ Important: - Password is stored in plain text - MUST be changed for
any real usage

------------------------------------------------------------------------

### 4. 🔐 Enables Auto Logon (1 time)

-   Automatically logs into `ladmin` after deployment
-   Useful for automation tasks

------------------------------------------------------------------------

### 5. 🧰 Runs Post-Deployment Commands

After first login, it runs commands to:

-   Prevent password expiration
-   Enable Remote Desktop
-   Configure firewall rules

------------------------------------------------------------------------

### 6. 🖥️ Applies System Tweaks (Registry)

Includes:

-   Disable Widgets
-   Disable Bing search in Start Menu
-   Enable Num Lock at login
-   Adjust Explorer defaults
-   Disable Windows suggestions

------------------------------------------------------------------------

### 7. 🌐 Enables Remote Desktop

-   Enables RDP connections
-   Opens firewall rules
-   Grants admin access

------------------------------------------------------------------------

## ⚠️ Limitations

This file:

-   Is NOT secure by default
-   Is NOT intended for enterprise production use
-   May behave differently depending on Windows edition

------------------------------------------------------------------------

## 🧠 Final Advice

This file is a **starting point**, not a final solution.

👉 Always adapt it to your environment and requirements.
