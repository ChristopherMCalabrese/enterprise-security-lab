# Project 04 – Lessons Learned

## Date

July 12, 2026

---

# Summary

Project 04 was completed successfully, but the lab experienced a significant infrastructure failure before validation was complete.

The root cause was **Proxmox LVM-Thin storage exhaustion**, which reached **100% utilization**. This resulted in multiple Windows VM issues that initially appeared unrelated.

---

# Symptoms Observed

## WIN11-01

- Intermittent RDP disconnects
- Console occasionally displayed a black screen
- VM continued running despite loss of connectivity

## DC01

- Failed to boot normally
- Entered Windows Recovery Environment
- Recovery environment could not initially access the system disk
- Active Directory appeared at risk until recovery was completed

## Proxmox

Attempting to clone a VM produced:

```
WARNING: Thin pool pve/data is out of data space.
Cannot create new thin volume.
```

This identified the underlying infrastructure issue.

---

# Root Cause

The Proxmox LVM-Thin pool reached **100% utilization**.

```
Data: 100%
```

At 100%, guest writes may fail, causing:

- Windows instability
- Filesystem corruption
- Snapshot failures
- VM cloning failures
- Unexpected recovery mode boots

This was the primary infrastructure issue.

---

# Investigation Performed

Verified:

- VM configuration
- VirtIO SCSI controller
- EFI partition
- TPM
- GPT partition table
- Windows Recovery Environment
- AD health
- DNS
- Replication
- Hypervisor configuration

Confirmed:

- Virtual disk existed
- GPT partition table intact
- EFI partition present
- Windows partition present
- Recovery partition present

---

# Resolution

## Extended the Thin Pool

```
lvextend -l +100%FREE /dev/pve/data
```

Storage changed from:

```
100%
```

to

```
75.71%
```

---

## Deleted Old Snapshots

Removed:

- Project-01-Complete
- Project-02-Complete
- Constant-disconnect-issue

Recovered approximately **23 GB** of thin-pool space.

---

## Rolled Back DC01

Restored:

```
Project04-GPO-Framework
```

After rollback:

- Active Directory started successfully
- DNS started successfully
- Netlogon started successfully

---

# Active Directory Validation

Verified:

```
dcdiag
```

Results:

- Connectivity ✔
- Advertising ✔
- DFSR ✔
- SYSVOL ✔
- Replication ✔
- RID Manager ✔
- DNS ✔
- Services ✔

Only remaining warning:

```
Generation ID changed
```

This is expected after restoring a virtualized domain controller snapshot.

---

# Lessons Learned

## 1. Monitor Thin Storage

LVM-Thin storage should never reach 100%.

Recommended warning levels:

| Usage | Action |
|--------|--------|
| 80% | Warning |
| 90% | Critical |

---

## 2. Do Not Keep RAM Snapshots

Memory snapshots consumed approximately:

```
16.5 GB
```

per snapshot.

Disk-only snapshots are sufficient for project milestones.

---

## 3. Keep Only One Milestone Snapshot

Recommended policy:

```
Project04-Completed

↓

Delete previous milestone

↓

Create Project05-Begin
```

Avoid accumulating snapshots.

---

## 4. Infrastructure Problems Can Mimic OS Failures

Symptoms initially suggested:

- Group Policy
- Windows Updates
- VirtIO drivers
- Active Directory corruption

Actual cause:

```
LVM-Thin Pool Full
```

Always verify hypervisor health before troubleshooting guest operating systems.

---

# Improvements Planned

- Configure LVM Thin Pool auto-extension
- Add Proxmox storage monitoring
- Alert when thin pool exceeds 80%
- Use disk-only snapshots
- Maintain one snapshot per completed project

---

# Outcome

Project 04 completed successfully.

The domain controller was recovered.

The workstation remained operational.

The lab storage configuration was improved.

Future projects will use a more resilient snapshot strategy and infrastructure monitoring.
