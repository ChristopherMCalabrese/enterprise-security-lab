# Case Study: Recovering an Unraid Array During a Parity Upgrade

## Summary

During a planned storage upgrade, I replaced the existing 16 TB parity drive in my Unraid server with a new 26 TB Seagate Exos drive. After the parity synchronization completed successfully, I repurposed the original parity drive as a data disk. Instead of joining the array immediately, Unraid began reconstructing the disk, which initially appeared to be a second parity rebuild.

Through command-line diagnostics, SMART analysis, and hardware validation, I confirmed the array was functioning correctly and that Unraid was performing the expected reconstruction process.

---

# Objectives

* Upgrade parity capacity from 16 TB to 26 TB.
* Increase future storage expansion capability.
* Reuse the former parity drive as an additional data disk.
* Maintain data integrity throughout the migration.

---

# Environment

**Platform**

* Unraid
* Supermicro X11SSL-CF
* Intel Xeon E3-1275 v6
* 64 GB ECC RAM
* Broadcom / LSI SAS3008 SAS Controller

**Storage**

* 1 × 26 TB Seagate Exos (Parity)
* 4 × 16 TB Seagate Exos
* 3 × 12 TB Western Digital

---

# Problem

The initial parity synchronization completed successfully after approximately two days.

After assigning the original parity drive as Disk 5, Unraid reported:

* Disk Invalid
* Reconstruction in progress
* `mdResyncAction=recon D5`

Initially, it appeared the system had unexpectedly started rebuilding the array again.

This raised several questions:

* Was parity rebuilding a second time?
* Had the replacement drive failed?
* Was there a hardware issue?
* Had the previous parity synchronization been unsuccessful?

---

# Investigation

To understand the array state, I began monitoring Unraid from the command line instead of relying solely on the WebGUI.

Using `mdcmd status` and `/proc/mdstat`, I confirmed the array was performing a **disk reconstruction** (`recon D5`) rather than rebuilding parity.

SMART diagnostics were collected from the replacement drive.

Results showed:

* SMART Passed
* No reallocated sectors
* No pending sectors
* No offline uncorrectable sectors

The only notable SMART attribute was a historical UDMA CRC error count, which was consistent with previous cabling issues rather than media failure.

Because the drive appeared healthy, I also validated the storage hardware.

The system uses an onboard Broadcom / LSI SAS3008 controller, and all data drives are connected through enterprise SAS breakout cables. SATA/SAS cabling had already been replaced earlier during troubleshooting, reducing the likelihood of a connectivity problem.

Throughout reconstruction, the array reported zero write errors and reconstruction progress continued normally.

---

# Recovery

After confirming reconstruction was proceeding normally, I restored production Docker services instead of waiting for reconstruction to complete.

Services returned to operation included:

* AdGuard Home
* UniFi Network Application
* Plex
* Home Assistant
* Grafana
* InfluxDB
* Vaultwarden
* Immich
* CrowdSec
* Wazuh
* Sonarr
* Radarr
* Prowlarr

This restored network functionality while allowing storage operations to continue uninterrupted.

---

# Additional Improvements

During this maintenance window I also configured the motherboard's onboard IPMI management controller.

Configuration included:

* Dedicated management interface
* DHCP reservation within OPNsense
* Remote HTML5 KVM console
* Remote power management
* Firmware verification

This provides full out-of-band management should the operating system become unavailable in the future.

---

# Outcome

The reconstruction completed successfully without media errors.

The array returned to a protected state with:

* 26 TB parity
* Restored Disk 5
* Production Docker services online
* Remote IPMI management fully configured

---

# Lessons Learned

This project reinforced several enterprise infrastructure concepts:

* Parity synchronization and disk reconstruction are separate maintenance operations.
* Understanding system state through command-line tools provides greater visibility than relying solely on graphical interfaces.
* SMART diagnostics should be interpreted in context rather than assumed to indicate hardware failure.
* Enterprise SAS controllers and ECC memory provide a reliable storage platform for long-running maintenance operations.
* Out-of-band management through IPMI significantly improves recoverability during infrastructure incidents.

---

# Skills Demonstrated

* Enterprise storage administration
* Linux command-line troubleshooting
* SMART diagnostics
* SAS storage management
* Hardware validation
* Docker service recovery
* Infrastructure documentation
* Operational decision making
* IPMI deployment
* Unraid storage management
