# Cybersecurity Lab Environment Setup

**Week 1 Project (WK1-PM1) - Networkwalks Cybersecurity Internship, Batch B083**

Building an isolated virtual lab for ethical hacking and penetration testing practice.
## Project Overview

This project sets up a virtual cybersecurity lab on my own laptop using **VirtualBox** and **Kali Linux**.

The purpose of the lab is to provide a controlled, isolated environment where security tools and techniques can be practiced safely and legally. The lab runs on a private virtual network, so more machines can be added later and used as targets for authorized testing.
## Lab Requirements and Result

| Requirement | Status |
|---|---|
| VirtualBox used as the base | Done |
| Kali Linux set up as the attacker machine | Done |
| Private network in subnet 10.0.0.0/24 | Done |
| NAT Network used with 10.0.0.0/24 | Done |
| Clipboard and drag & drop enabled | Done |
| Shared folder from the host (Downloads) | Done |
| Kali Linux IP address is 10.0.0.2/24 | Done |
| Kali Linux has full internet access | Done |
| Snapshot of the VM taken | Done |
## Lab Architecture

| Item | Details |
|---|---|
| Host OS | Windows |
| Hypervisor | Oracle VirtualBox |
| Attacker VM | Kali Linux 2026.3 (amd64) |
| Network type | NAT Network (named `NatNetwork`) |
| Subnet | 10.0.0.0/24 |
| Kali IP | 10.0.0.2/24 |
| Gateway | 10.0.0.1 |
| DNS | 10.0.0.1 |
## Step-by-Step Setup
### Step 1: Install VirtualBox

Downloaded and installed the latest VirtualBox from the official website on my Windows laptop.

### Step 2: Create the NAT Network

In VirtualBox, I went to Tools > Network > NAT Networks and created a network named NatNetwork with the IPv4 prefix 10.0.0.0/24 and DHCP enabled.
<img width="974" height="645" alt="02-natnetwork-created" src="https://github.com/user-attachments/assets/01af9649-9157-4234-81f7-693d5d948cbd" />

### Step 3: Import Kali Linux
Downloaded the pre-built Kali Linux VirtualBox image from the official Kali website and imported it into VirtualBox.
<img width="1920" height="1080" alt="01-kali-desktop" src="https://github.com/user-attachments/assets/950afef9-ad02-4096-98b5-612f3026d51c" />

### Step 4: Attach Kali to the NAT Network
In the Kali VM **Settings > Network**, Adapter 1 is attached to **NAT Network** (`NatNetwork`), with Promiscuous Mode set to **Allow All**.
<img width="974" height="643" alt="03-kali-network-adapter" src="https://github.com/user-attachments/assets/8a89d1eb-867d-4ad2-a394-281be9be66f2" />

### Step 5: Configure the static IP on Kali
In Kali, I opened **Edit Connections** and set the IPv4 method to **Manual**:

- Address: `10.0.0.2`
- Netmask: `24`
- Gateway: `10.0.0.1`
- DNS: `10.0.0.1`
<img width="703" height="547" alt="04-kali-ipv4-settings" src="https://github.com/user-attachments/assets/cf2514d6-3696-441c-846d-2f67ed643336" />

### Step 6: Test internet access
Ran `ping -c 4 google.com` from the Kali terminal. All 4 packets were received with 0% packet loss, confirming full internet access.
<img width="1920" height="1080" alt="05-internet-ping-test" src="https://github.com/user-attachments/assets/713c333c-0e4c-4ee8-9b11-a3852f4ed0c6" />

### Step 7: Enable clipboard and drag & drop
In **Settings > General > Features**, set both **Shared Clipboard** and **Drag-and-Drop** to **Bidirectional**.
<img width="978" height="644" alt="06-clipboard-dragdrop" src="https://github.com/user-attachments/assets/f10b4331-faa7-4763-b79f-610ea8d620c1" />

### Step 8: Enable the shared folder
In **Settings > Shared Folders**, added the host **Downloads** folder with Full access and Auto Mount enabled.
<img width="978" height="642" alt="07-shared-folder-downloads" src="https://github.com/user-attachments/assets/4579cfe0-462f-4c86-852e-bf25605f49a2" />

### Step 9: Take a snapshot
Took a VM snapshot so I can always restore a clean, working state of the lab.
<img width="1920" height="1080" alt="08-snapshot" src="https://github.com/user-attachments/assets/56c39fc9-a9f0-4127-86d3-c0a5f39077f5" />

## Troubleshooting

I did not face any major issues during this setup. To avoid problems, I checked each step as I went:

- Confirmed the NAT Network was created with the correct 10.0.0.0/24 prefix
- Checked that no other VM was using the same IP address
- Tested internet access with a ping to google.com right after setting the static IP

Known issue to watch for: on VirtualBox 7 with newer Kali versions, a static IP can sometimes cause the internet to drop. Changing the DNS server or adjusting the NetworkManager DAD timeout setting with nmcli, then restarting Kali, can fix this.

## What I Learned

- How virtual networking works in VirtualBox, including NAT Networks and subnets
- How to configure a static IP address on Kali Linux
- Why an isolated lab is important for safe and legal security practice
- How snapshots protect the lab from mistakes
- How to troubleshoot network connectivity step by step

## Author

**Oshadhee Anupama Thalagoda**\
Cybersecurity Internship B084

LinkedIn:www.linkedin.com/in/oshadhee-thalagoda-861b2329b






