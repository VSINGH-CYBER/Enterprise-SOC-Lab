# 00 - Lab Setup (v1)

## Objective
Build a reusable enterprise-style home lab used across all portfolio projects (AD hardening, SIEM ingestion, attack simulation, vuln management, detection engineering).

## Architecture Overview
**Core Systems**
- Windows Server 2022: Domain Controller (AD DS, DNS)
- Windows 10: Domain-joined workstation
- Kali Linux: Attacker / testing host
- Wazuh: SIEM + endpoint monitoring

## Network Plan
| Component | Role | IP (Planned) | Notes |
|---|---|---:|---|
| DC01 | Domain Controller |  | Static IP |
| WIN10-01 | Client |  | DHCP or static |
| KALI-01 | Attacker |  | Same lab VLAN |
| WAZUH-01 | SIEM |  | Static IP recommended |

> Note: IPs will be finalized after VM creation.

## Build Steps (Initial)
### 1) Create VMs
- [ ] Create Windows Server 2022 VM (DC01)
- [ ] Create Windows 10 VM (WIN10-01)
- [ ] Create Kali Linux VM (KALI-01)
- [ ] Create Wazuh VM (WAZUH-01)

### 2) Configure Virtual Networking
- [ ] Create isolated lab network (internal / host-only)
- [ ] Confirm all VMs can ping each other
- [ ] Confirm internet access is available only if intended (document choice)

### 3) Baseline Snapshots
- [ ] Snapshot: “Fresh OS Install” for each VM
- [ ] Snapshot: “Network Verified” once connectivity confirmed

## Evidence
Screenshots will be stored in:
- `00-Lab-Setup/screenshots/`

Recommended screenshots:
- VM list showing all machines created
- IP config from each machine
- Successful ping tests between machines
- Snapshot manager showing baseline snapshots

## Lessons Learned / Notes
- (Place Notes here)

## Network Configuration

### Internal LAN (VMnet1)
- Subnet: 192.168.100.0/24
- DHCP: Disabled
- Purpose: Isolated enterprise lab network

### Planned Static IP Assignments
| Machine | Role | IP |
|----------|------|------|
| DC01 | Domain Controller | 192.168.100.10 |
| WIN10-01 | Client | 192.168.100.20 |
| WAZUH-01 | SIEM | 192.168.100.30 |
| KALI-01 | Attacker | 192.168.100.40 |

## Evidence

### VMware Network (VMnet1)
![VMnet1 Configuration](screenshots/01_vmnet1_configuration.png)

### DC01 VM Summary
![DC01 Final VM Summary](screenshots/02_dc01_final_vm_summary.png)

### DC01 VM Created
![DC01 VM Created](screenshots/03_dc01_vm_created.png)

## DC01 Infrastructure Provisioning

### Purpose
DC01 will serve as the primary Domain Controller for the Enterprise SOC Lab environment. It will later host:
- Active Directory Domain Services (AD DS)
- DNS
- Group Policy (GPOs)
- Centralized user/admin identity management

### Configuration Decisions
| Component | Value |
|---|---|
| VM Name | DC01 |
| OS | Windows Server 2022 (Evaluation ISO) |
| CPU | 2 vCPU (2 cores) |
| RAM | 4 GB |
| Disk | 60 GB (Thin provisioned) |
| Disk Bus | SCSI (LSI Logic SAS) |
| Network | VMnet1 (Host-Only) |
| Firmware | UEFI |
| Storage Location | E:\Enterprise-SOC-Lab\VMs\DC01 |

### Why This Matters
- **Host-only networking** isolates lab traffic from the home network (safe attacker testing later).
- **Static addressing (DHCP disabled)** keeps logs consistent for SIEM + investigations.
- **Thin-provisioned disk** saves space while allowing growth (snapshots + logs).

### Evidence
![VMnet1 Configuration](screenshots/01_vmnet1_configuration.png)  
![DC01 Final VM Summary](screenshots/02_dc01_final_vm_summary.png)  
![DC01 VM Created](screenshots/03_dc01_vm_created.png)

