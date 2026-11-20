# NETWORKWALKS-YUSUF-B083-WK1-PM1-CYBERSECURITY-LAB-SETUP
Cyber Security Lab setup
# Cybersecurity Home Lab: Kali, Windows 10 and Android on VirtualBox

Three virtual machines on one isolated network, built to practice network testing and penetration testing.

## Lab Setup

| Machine | Role | IP Address |
|---|---|---|
| Kali Linux | Testing machine | 10.0.0.2 |
| Windows 10 | Target | 10.0.0.10 |
| Android | Mobile target | 10.0.0.9 |

- **Host:** Oracle VirtualBox
- **Network:** NAT Network (`NatNetwork`), 10.0.0.0/24, DHCP off

## Downloads

| Software | Source |
|---|---|
| VirtualBox | https://www.virtualbox.org/wiki/Downloads |
| Kali Linux (ISO) | https://www.kali.org/get-kali/ |
| Windows 10 (ISO) | https://www.microsoft.com/software-download/windows10 |
| Android (ISO) | https://sourceforge.net/projects/android-x86/files/latest/download |

**VirtualBox**
1. Open the VirtualBox downloads page.
2. Click **Windows hosts** (or your host operating system).
3. Run the installer and accept the default options.

**Kali Linux**
1. Open the Kali download page and select **Installer Images**.
2. Download the 64-bit installer ISO.

**Windows 10**
1. Open the Microsoft Windows 10 download page.
2. Click **Download tool now** to get the Media Creation Tool, and run it.
3. Select **Create installation media for another PC**.
4. Choose your language, edition and **64-bit**.
5. Select **ISO file** and choose where to save it.

**Android**
1. Open the Android download page linked above.
2. Download the 64-bit ISO.

## Setup Steps

1. In VirtualBox, go to **File > Tools > Network Manager > NAT Networks** and create `NatNetwork` with prefix `10.0.0.0/24` and DHCP off.
2. Create a new VM for each system (Kali, Windows 10, Android) from its ISO.
3. For each VM, go to **Settings > Network**, set **Attached to** to `NAT Network`, and select `NatNetwork`.
4. Install each operating system.
5. Set a static IP on each machine (subnet `255.255.255.0`, gateway `10.0.0.1`).


## Ping Tests

Windows blocks ping by default. On Windows 10, run this in Command Prompt as Administrator first:

```
netsh advfirewall firewall add rule name="Allow ICMPv4" protocol=icmpv4:8,any dir=in action=allow
```

| Test | Source | Destination | Command | Result |
|---|---|---|---|---|
| 1 | Windows 10 | Kali | `ping 10.0.0.2` | Success |
| 2 | Kali | Windows 10 | `ping -c 4 10.0.0.10` | Success |
| 3 | Android | Kali | `ping -c 4 10.0.0.2` | Success |
| 4 | Kali | Android | `ping -c 4 10.0.0.9` | Success |


<img width="960" height="516" alt="Screenshot 2026-11-18 133741" src="https://github.com/user-attachments/assets/4976a71a-0afb-4600-bb10-2cdbe9bb3572" />

<img width="960" height="516" alt="Screenshot 2026-11-18 134629" src="https://github.com/user-attachments/assets/454ba3f9-4e83-4e1d-83b4-3aad4d6c5434" />


<img width="960" height="516" alt="Screenshot 2026-11-17 105559" src="https://github.com/user-attachments/assets/6f4ed166-0907-459c-b441-dd8e211ea045" />

<img width="960" height="516" alt="Screenshot 2026-11-17 105622" src="https://github.com/user-attachments/assets/24a4d0a1-f60b-4530-be96-75f9d903afbf" />


## What I Learned

- How to build an isolated virtual network in VirtualBox
- How to assign static IPs and verify connectivity with ping
- How firewalls affect ICMP traffic
