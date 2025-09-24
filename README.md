# Proxmox VE Kursus - Orange Makers

## Kursusagenda

## Hvorfor Virtualisering?

Virtualisering har revolutioneret IT-verdenen siden 1960'erne, hvor IBM introducerede konceptet på mainframes. 
I dag er det fundamentet for moderne datacentre og cloud computing.

**Historisk udvikling:**
- 1960'erne: IBM mainframes - første virtuelle maskiner
- 1990'erne: VMware bringer virtualisering til x86 arkitektur
- 2000'erne: Hypervisorer bliver mainstream (VMware ESX, Microsoft Hyper-V)
- 2010'erne: Cloud computing boom - AWS, Azure, Google Cloud
- I dag: Containers (Docker/Kubernetes) og edge computing

**Hvorfor virtualisere?**
- **Ressourceoptimering** - Én fysisk server kan køre mange virtuelle maskiner
- **Isolering** - Applikationer påvirker ikke hinanden
- **Fleksibilitet** - Nem migration og backup af hele systemer
- **Omkostningsbesparelse** - Færre fysiske servere, lavere strømforbrug
- **Testmiljøer** - Hurtig oprettelse og nedlukning af test-systemer
- **Disaster Recovery** - Nem gendannelse ved nedbrud

Proxmox VE kombinerer KVM virtualisering med LXC containers i én open-source platform.

### 1. Proxmox VE Installation
- Download og installation af Proxmox VE 9
- **Download:** [Proxmox VE 9 ISO](https://www.proxmox.com/en/downloads/proxmox-virtual-environment)
- Grundlæggende opsætning under installation
- Første boot og login

### 2. Post-Installation Optimering
- Anvendelse af Community Scripts til optimering
- Kør Post-PVE Install script for performance tuning
- **Link:** [Post-PVE Install Script](https://community-scripts.github.io/ProxmoxVE/scripts?id=post-pve-install)
- **Community Scripts:** [ProxmoxVE Scripts](https://community-scripts.github.io/ProxmoxVE/)

### 3. Proxmox UI Gennemgang
- Navigation i webinterfacet
- Netværkskonfiguration
- Storage management
- Node og cluster oversigt
- Grundlæggende indstillinger

### 4. Første VM Oprettelse
- Upload af ISO filer
- VM oprettelse step-by-step
- Hardware konfiguration
- Netværksopsætning
- Start og administration af VM

#### 4.1 Ubuntu VM
- **Anbefalede indstillinger:**
  - OS Type: Linux 6.x/2.6 Kernel
  - BIOS: OVMF (UEFI)
  - Machine: q35
  - SCSI Controller: VirtIO SCSI single
  - Hard Disk: VirtIO Block
  - Network: VirtIO (paravirtualized)
  - Display: SPICE eller VGA
- **Download:** [Ubuntu Server LTS](https://ubuntu.com/download/server)
- **Post-Installation:** Installer QEMU Guest Agent for bedre integration
  ```bash
  sudo apt update && sudo apt install qemu-guest-agent
  sudo systemctl enable qemu-guest-agent
  sudo systemctl start qemu-guest-agent
  ```
  - Aktiver "QEMU Guest Agent" i VM Options efter installation

#### 4.2 Windows VM
- **Anbefalede indstillinger:**
  - OS Type: Microsoft Windows 11/2022
  - BIOS: OVMF (UEFI) + TPM
  - Machine: q35
  - SCSI Controller: VirtIO SCSI single
  - Hard Disk: VirtIO Block + Cache: Write back
  - Network: VirtIO (paravirtualized)
  - Display: SPICE
- **VirtIO Drivers:** [Windows VirtIO Drivers](https://pve.proxmox.com/wiki/Windows_VirtIO_Drivers)
- **Download:** [Windows 11 ISO](https://www.microsoft.com/software-download/windows11)
- **Post-Installation:** 
  - Installer VirtIO drivers for optimal performance
  - QEMU Guest Agent er inkluderet i VirtIO driver pakken
  - Aktiver "QEMU Guest Agent" i VM Options efter installation

### 5. SPICE Installation og Opsætning
- Installation af SPICE klient
- Konfiguration for optimal performance
- Forbindelse til VMs via SPICE
- **Link:** [SPICE Documentation](https://pve.proxmox.com/wiki/SPICE)

## Nyttige Links
- [Proxmox VE Documentation](https://pve.proxmox.com/pve-docs/)
- [Community Scripts Repository](https://community-scripts.github.io/ProxmoxVE/)
- [Proxmox VE 9 Release Notes](https://pve.proxmox.com/wiki/Roadmap#Proxmox_VE_9.x)

## Målgruppe
Basic niveau - ingen forkundskaber krævet