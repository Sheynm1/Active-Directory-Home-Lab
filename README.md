https://github.com/Sheynm1/Active-Directory-Home-Lab/blob/a7f072c8b19f605b54c164136ba09131f2eb9a63/Active_Directory_Practice_Home_Lab.png

This repository guides you through setting up a basic **Active Directory (AD)** home lab using either Oracle VirtualBox or VMware. This was done for practice and preperation for COMPTIA and Future certifications.

---

## 🛠️ Lab Overview

- **Domain Controller**: Windows Server 2019 
- **Clients**: Windows 10 
- **Virtualization**: VirtualBox 
- **Network Type**: Internal and Host-Only Adaptor

---

## 🖼️ Lab Diagram

![Lab Network Diagram](Desktop/Networkdiagram.png)

---

## 💾 Requirements

| Component         | Minimum Specs                |
|------------------|------------------------------|
| RAM              | 8–16 GB                      |
| Disk Space       | 80+ GB                       |
| VirtualBox/VMware| Latest version               |
| ISO Files        | Windows Server 2019 + Windows 10  |

---

## 🏗️ Setup Steps

## Domain Controller (Windows Server 2019)

- Create a **Domain Controller VM** using Windows Server 2019 in VirtualBox.
- Assign **two network interfaces**:
  - **NAT** for internet access
  - **Internal Network** for lab communication

## Windows Server Configuration

- Install Windows Server OS on the VM.
- Assign a **static IP address** (`IP: 172.16.0.1, Mask: 255.255.255.0`).
- **Rename the host** to something like `DC`.

## Promote to Domain Controller

- Install **Active Directory Domain Services (AD DS)**.
- Promote the server to a domain controller:
  - Create a **new forest** and **domain** (Name it `mydomain.com`)
  - Set the **DSRM (Directory Services Restore Mode)** password to `something memorable`

## DNS Setup

- Configure DNS to **point to itself** using the loopback address (`127.0.0.1`).

## Active Directory Structure

- Create a new **Organizational Unit (OU)** for admins(Name it `ADMINS`).
- Create an **admin user** inside the OU(`This can be yourself!`).
- Add the admin user to the **Domain Admins** group.

## Network Routing (Optional)

- Install and configure **Routing and Remote Access** to provide NAT.
- This allows internal network clients to **access the internet** through the DC.

## DHCP Server Setup

- Install the **DHCP Server** role.
- Create a new **DHCP scope** (e.g., `172.16.0.100 – 172.16.0.200`).
- Configure DHCP options:
  - Gateway - `172.16.0.1`
  - DNS - `172.16.0.1`
  - Lease duration - `8 days`

## Bulk User Creation

- Use a **PowerShell script** and a `.txt` file with names to create **1,000 users**.
- Users are added to specific OUs.

## Client Machine Setup

- Build a **Windows 10 VM**.
- Connect it to the **internal network**.
- Join the domain (`mydomain.com`).
- Log in with a domain account to **verify domain connectivity**.

## Final Verification

- Open **Active Directory Users & Computers** and verify that all user accounts were created.
- Check the **DHCP lease assignments** to confirm client connectivity.
