# NimbusStack
An open, lightweight cloud platform designed to create and manage virtualized infrastructure with simplicity and scale in mind – from a single node to global cloud deployments.


## PHASE 1: PREPARE YOUR HARDWARE & NETWORK
Requirements
- Machine: Desktop/Laptop with:
        ◦ 64-bit CPU with virtualization support (Intel VT-x or AMD-V)
        ◦ 8GB+ RAM (16GB recommended)
        ◦ 250GB+ SSD
- Network: Stable wired internet connection preferred.
- Second computer or same machine with dual boot to access Proxmox dashboard after install.

## PHASE 2: DOWNLOAD & PREPARE PROXMOX
    1. Download Proxmox VE ISO
https://www.proxmox.com/en/downloads
        ◦ Choose Proxmox VE ISO Installer (latest stable version).
    2. Create Bootable USB
        ◦ Windows: Use Rufus.
        ◦ Linux: Use dd or Etcher.
    3. BIOS Settings
        ◦ Enable Virtualization (Intel VT-x or AMD-V).
        ◦ Set USB as boot priority.

## PHASE 3: INSTALL PROXMOX VE
    1. Boot from USB → Select Install Proxmox VE.
    2. Disk Selection: Choose disk for Proxmox installation (⚠ this will erase it).
    3. Country & Time Zone: Set appropriately.
    4. Password: Root password + email for admin.
    5. Networking: Set static IP (example: 192.168.1.100).
    6. Finish Installation and reboot.

## PHASE 4: ACCESS PROXMOX DASHBOARD
    1. From another machine (or same if dual boot), open browser:
       https://<Proxmox-IP>:8006
       Example:
       https://192.168.1.100:8006
    2. Login:
        ◦ User: root
        ◦ Password: (set during installation)

## PHASE 5: SETUP STORAGE & NETWORK
Storage
    • Go to Datacenter → Storage.
    • Ensure you have:
        ◦ local-lvm → VM disks
        ◦ local → ISO images/templates
Networking
    • Default bridge vmbr0 created automatically (works for LAN and internet).
    • If using Wi-Fi, ensure bridging is enabled.

## PHASE 6: UPLOAD VM TEMPLATE
    1. Go to Datacenter → Node → local → ISO Images.
    2. Upload an OS ISO (example: Ubuntu Server ISO).
    3. Use this template for new virtual machines.

## PHASE 7: CREATE YOUR FIRST VIRTUAL MACHINE (VM)
    1. Click Create VM:
        ◦ Node: Your Proxmox node
        ◦ VM ID: Auto-generated (e.g., 100)
        ◦ Name: ubuntu-server-01
    2. OS: Select uploaded Ubuntu ISO.
    3. System: Default settings (BIOS: SeaBIOS or OVMF for UEFI).
    4. Hard Disk: Select local-lvm, 20GB+ recommended.
    5. CPU & Memory: 2 cores, 2GB RAM (adjust to your hardware).
    6. Network: vmbr0 (default).
    7. Finish → Start VM.

## PHASE 8: INSTALL OS INSIDE VM
    • Open console from Proxmox UI.
    • Install Ubuntu or preferred OS as normal.

## PHASE 9: ACCESS VM VIA SSH
    1. Get IP:
       ip a
    2. From another machine:
       ssh user@<vm-ip>

## PHASE 10: YOUR MINI CLOUD IS READY
    • You can now:
        ◦ Create multiple VMs (like AWS EC2 instances).
        ◦ Stop/Start/Reset from dashboard.
        ◦ Clone templates for fast deployments.

OPTIONAL: BUILD CUSTOM WEB INTERFACE (AWS-like)
    • Use Proxmox API to control VMs programmatically:
        ◦ API endpoint: https://<Proxmox-IP>:8006/api2/json/
    • Build a Flask web interface to:
        ◦ List all VMs
        ◦ Start/Stop VMs
        ◦ Show resource usage

## SECURITY & BACKUP
    1. Change default port if exposing online.
    2. Enable 2FA for Proxmox.
    3. Setup backup jobs for VM snapshots.

## RESULT
You now have:
    • Your own cloud platform running locally.
    • A web console to create and manage virtual servers.
    • Foundation to later:
        ◦ Add object storage (Ceph)
        ◦ Add load balancer
        ◦ Expand to multiple nodes (like AWS availability zones).


