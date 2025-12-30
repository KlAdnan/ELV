# ONVIF - Universal Standard for Security Cameras

## What is ONVIF?

If you are setting up a home or business security system, look for the ONVIF logo on cameras and NVRs (Network Video Recorders). If both devices are ONVIF-compliant, you can usually plug a Hikvision camera into a Dahua recorder, or use a Bosch camera with Milestone software, and they will work without complex custom coding.

## ONVIF Logo Examples

![ONVIF Logo 1](onvif.jpeg)

![ONVIF Logo 2](onvif.png)

## Benefits of ONVIF

- **Interoperability**: Mix and match different brands
- **No vendor lock-in**: Freedom to choose best devices
- **Easy integration**: Works without custom programming
- **Industry standard**: Widely supported by major manufacturers

---

# VLANs: Virtual Local Area Networks

Creating Logical Segmentation on a Shared Physical Infrastructure

## What is a VLAN?

A VLAN (Virtual Local Area Network) allows you to logically divide a single physical switch into multiple broadcast domains. This means devices on different VLANs cannot communicate directly, even though they're connected to the same switch - providing security, performance, and flexibility benefits.

![VLAN Overview](vlan%202.png)

## VLAN Configuration Example

### Configuration Commands:

```
Switch(config)# vlan 5
Switch(config-vlan)# name Sales
Switch(config-vlan)# exit
Switch(config)# interface range fa0/1 - 4
Switch(config-if-range)# switchport access vlan 5

Switch(config)# vlan 10
Switch(config-vlan)# name Marketing
Switch(config-vlan)# exit
Switch(config)# interface range fa0/5 - 8
Switch(config-if-range)# switchport access vlan 10
```

![VLAN Configuration Example](vlan.jpg)

## Key VLAN Benefits

- **Security (Isolation)**: Limits broadcast traffic and enhances security
- **Performance (Efficiency)**: Reduces broadcast domains for better network speed
- **Flexibility (Logical Grouping)**: Easily group devices regardless of physical location

## How VLANs Work

1. **Step 1: Access & Configure** - Connect to the managed switch
2. **Step 2: Define the VLAN** - Create VLAN with ID and name
3. **Step 3: Assign Ports to VLAN** - Configure which physical ports belong to the VLAN
4. **Step 4: Verify Configuration** - Check VLAN status with `show vlan brief`

---

# NVR: Network Video Recorder Setup Guide

## What is an NVR?

A Network Video Recorder (NVR) is a specialized computer system that records video from IP cameras to a hard disk drive (HDD). Unlike DVRs that process video at the recorder, NVRs work with IP cameras that encode and process video at the camera level, then stream it to the NVR for storage and viewing.

📄 **[Complete Setup Guide - Download PDF](NVR_Setup_Box_to_Live_View.pdf)**

## Dahua NVR Setup: From Box to Live View

### Hardware Installation

#### Step 1: Install Hard Drive
- Open the NVR chassis
- Mount surveillance-grade HDD (check max capacity: 10TB for 4116, varies for 4216)
- Connect SATA and power cables
- **Pro Tip**: Use surveillance-grade drives optimized for 24/7 recording

#### Step 2: Make Physical Connections
- **Mouse**: Connect USB mouse (front or rear port)
- **Network (LAN)**: Connect to router/switch via Ethernet cable (CRITICAL for remote viewing)
- **Power**: Connect power supply (external 48V for 4116, built-in for 4216)
- **Monitor**: Connect via HDMI or VGA (can use both simultaneously)
- **PoE Camera Ports**: Plug cameras directly for auto-detection and power

### Network Architecture Options

| Scenario | Setup | Use Case |
|----------|-------|----------|
| **A: Standalone** | Cameras → NVR PoE ports only | Local monitor viewing, no network needed |
| **B: Expanded Local** | Cameras → PoE Switch ← NVR | More cameras than NVR ports, PC access on LAN |
| **C: Full Remote** | Cameras → PoE Switch → Router → Internet | Remote viewing from anywhere via phone/web |

### Network Configuration Essentials

**Understanding Your Network Address**:
- **IP Address**: Unique device address (e.g., 192.168.1.108)
- **Subnet Mask**: Network range definition (typically 255.255.255.0)
- **Default Gateway**: Router IP for internet access (e.g., 192.168.1.1)

### Initial Setup Wizard

**Step 1**: Region & Language Selection
**Step 2**: Set Strong Admin Password (8-32 characters)
**Step 3**: Create Unlock Pattern (optional)
**Step 4**: CRITICAL - Set Recovery Email (only way to reset password)
**Step 5**: Device Name & Enable NTP for auto time sync

### Static vs DHCP IP Configuration

✅ **Static IP (Recommended)**:
- IP address never changes
- Reliable remote access
- Example: 192.168.8.253
- Always click "Test" to verify availability

⚠️ **DHCP (Not Recommended)**:
- IP can change on reboot
- Breaks remote access connections
- Only use for temporary setups

### Enable P2P for Easy Remote Access

**What is P2P?**: Peer-to-Peer service allows mobile app to find your NVR without complex port forwarding

**Setup**:
1. Enable P2P in setup wizard
2. Verify status shows "Online"
3. Use QR code to add device to mobile app
4. ⚠️ **Keep QR code and serial number private!**

### Camera Registration

**Automatic Detection**:
- Cameras plugged into NVR PoE ports auto-detect
- NVR uses its admin password to login

**Manual Addition**:
- NVR scans network for Dahua cameras
- Manually add via Camera menu
- If status shows error, verify camera password matches

### Recording Schedule Configuration

**Storage Settings**:
- Set to "Overwrite" mode (auto-deletes oldest footage when full)
- Avoid "Stop Record" (halts all recording when drive full)

**Schedule Options**:
- **Regular (Green)**: 24/7 continuous recording
- **MD (Yellow)**: Motion Detection only (saves space)

**Recommended Setup for Space Saving**:
1. Remove default Regular schedule
2. Enable MD (Motion Detection)
3. Fill entire schedule with MD
4. Use "Copy" to apply to all channels

### Mobile App Setup (gDMSS/iDMSS)

1. Download **gDMSS Plus** (Android) or **iDMSS Plus** (iOS)
2. Open app → Add device
3. Select **SNScan**
4. Scan **Device SN QR code** from NVR monitor (Network → P2P)
5. Start Live View

### Video Streams Explained

| Stream Type | Resolution | Bitrate | Use Case |
|-------------|------------|---------|----------|
| **Main Stream** | Full (1920x1080+) | High | Recording to HDD |
| **Sub Stream** | Lower (D1) | Low | Mobile/remote viewing (less bandwidth) |

**Configuration**: Camera → Encode settings

### PC Access Methods

**Method 1: Web Browser**
- Type NVR IP in browser: `http://192.168.8.253`
- Access: Live view, playback, configuration

**Method 2: Smart PSS Software**
- Download from Dahua website (Windows/macOS)
- Centralized management for multiple NVRs
- Advanced features and controls

---

# SIRA/ADMCC: UAE Security Camera Requirements (C025 Standards)

## Overview

![SIRA UAE Security Camera Requirements](sira.png)

Compliant with **SIRA** (Dubai) and **MCC/ADMCC** (Abu Dhabi) regulations introduced in **Administrative Resolution No. (13) April 2025**.

## SIRA CCTV Network Isolation (VLAN 100)

- [ ] All cameras and NVRs on isolated VLAN (100)
- [ ] Layer 3 managed switch deployed
- [ ] Strong passwords enabled on all devices
- [ ] SSH enabled, Telnet disabled
- [ ] Configuration saved to startup-config
- [ ] Network diagram documented
- [ ] Admin credentials securely stored
- [ ] Regular firmware updates scheduled
- [ ] Access logs monitored

---

## Key Takeaways

✅ **ONVIF**: Universal standard for camera/NVR interoperability  
✅ **VLANs**: Network segmentation for security and performance  
✅ **NVR**: Complete setup from hardware to mobile viewing  
✅ **SIRA/ADMCC**: UAE compliance with proper network isolation  

**All systems properly configured and operational!**
