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

## Forudsætninger (Prerequisites)

### Hardware Krav
- **CPU:** 64-bit processor med virtualisering support
- **RAM:** Minimum 2GB (anbefalet 4GB+)
- **Storage:** Minimum 32GB ledig plads
- **Netværk:** Ethernet forbindelse

### BIOS/UEFI Konfiguration
**VIGTIGT:** Før installation skal virtualisering aktiveres i BIOS/UEFI!

**Intel processorer:**
- Intel VT-x (Intel Virtualization Technology)
- Intel VT-d (for device passthrough - valgfrit)

**AMD processorer:**
- AMD-V (AMD Virtualization)
- AMD-Vi/IOMMU (for device passthrough - valgfrit)

**Sådan tjekker og aktiverer du VT:**
1. Genstart computeren og gå ind i BIOS/UEFI (typisk F2, F12, DEL under boot)
2. Find "Advanced" eller "CPU Configuration" menuen
3. Look for "Intel VT-x", "AMD-V", "Virtualization Technology" eller lignende
4. Aktiver funktionen (Enable)
5. Gem og genstart (Save & Exit)

**Note:** Nogle systemer har VT aktiveret som standard, men det er altid godt at tjekke først.

### 1. Proxmox VE Installation
- Download og installation af Proxmox VE 9
- **Download:** [Proxmox VE 9 ISO](https://www.proxmox.com/en/downloads/proxmox-virtual-environment)
- Grundlæggende opsætning under installation
- Første boot og login

#### 1.1 Netværkskonfiguration til Demo
- **IP Adresse:** 172.17.3.15/24
- **DNS Servere:** CloudFlare DNS
  - Primary: 1.1.1.1
  - Secondary: 1.0.0.1
- **Gateway:** 172.17.3.1

#### 1.2 Adgang til Admin Interface
Efter vellykket installation kan du tilgå Proxmox VE web interface på:
- **URL:** [https://172.17.3.15:8006](https://172.17.3.15:8006)
- **Brugernavn:** root
- **Password:** Det password du satte under installationen
- **Note:** Accepter SSL certifikat advarslen i browseren (self-signed certificate)

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

## Optional Knowledge - Andre Proxmox Produkter

### Proxmox Backup Server (PBS)
- Dedikeret backup løsning til Proxmox VE
- Deduplicering og kryptering af backups
- Incremental backups med snapshot funktionalitet
- Integration med Proxmox VE for automatiserede backups
- **Link:** [Proxmox Backup Server](https://www.proxmox.com/en/proxmox-backup-server)

### Proxmox Mail Gateway (PMG)
- Mail security gateway til spam og virus beskyttelse
- Anti-spam og anti-virus scanning
- Greylistning og DNSBL funktionalitet
- Web-baseret administration interface
- Integration med eksisterende mail infrastruktur
- **Link:** [Proxmox Mail Gateway](https://www.proxmox.com/en/proxmox-mail-gateway)

### Proxmox Cluster Integration
- Cluster funktionalitet for High Availability (HA)
- Live migration af VMs mellem nodes
- Delt storage og automatisk failover
- Centraliseret management af flere Proxmox servere

## Målgruppe
Basic niveau - ingen forkundskaber krævet