# 🔌 Zigbee2MQTT Setup Guide

Complete guide for adding Zigbee device control to your AI-powered Home Assistant setup.

## 📋 Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Quick Start](#quick-start)
- [Detailed Setup](#detailed-setup)
- [Troubleshooting](#troubleshooting)
- [Device Pairing](#device-pairing)
- [Integration with AI](#integration-with-ai)

---

## 🎯 Overview

**Zigbee2MQTT** allows you to control Zigbee devices (lights, sensors, switches, etc.) through Home Assistant without needing proprietary hubs.

### Why Zigbee2MQTT?

- ✅ **3000+ supported devices** (vs ~500 for ZHA)
- ✅ **Web UI** for easy device management
- ✅ **Local control** - no cloud dependency
- ✅ **Active development** and community support
- ✅ **Network visualization** to see device mesh
- ✅ **OTA updates** for device firmware

---

## 🔧 Prerequisites

### Hardware Requirements

**USB Zigbee Coordinator** (one of the following):
- ⭐ **Sonoff Zigbee 3.0 USB Dongle Plus V2** (~$15-20) - Recommended
- ConBee II (~$40)
- CC2652RB Stick (~$25)
- HUSBZB-1 (Zigbee + Z-Wave combo)

### Software Requirements

- Home Assistant OS 16.2+
- Terminal & SSH add-on (for configuration)
- MQTT integration enabled

---

## ⚡ Quick Start

### 1. Install Zigbee2MQTT Add-on

1. **Open Home Assistant**: http://192.168.0.166:8123
2. **Go to**: Settings → Add-ons → Add-on Store
3. **Search**: "Zigbee2MQTT"
4. **Install**: "Zigbee2MQTT" (by Zigbee2MQTT)
5. **Wait**: ~2 minutes for installation

### 2. Configure USB Device

Before starting the add-on:

1. **Check your USB device** (in Terminal add-on):
   ```bash
   ls -la /dev/serial/by-id/
   ```

2. **Copy the device path**, for example:
   ```
   /dev/serial/by-id/usb-Itead_Sonoff_Zigbee_3.0_USB_Dongle_Plus_V2_52d547cd3fd9ee11a653ab4c37b89984-if00-port0
   ```

3. **Go to**: Settings → Add-ons → Zigbee2MQTT → Configuration

4. **Update the serial port**:
   ```yaml
   serial:
     port: /dev/serial/by-id/usb-Itead_Sonoff_Zigbee_3.0_USB_Dongle_Plus_V2_YOUR_ID_HERE-if00-port0
     adapter: auto
   ```

5. **Optional: Set web UI port** (if 8099 is in use):
   ```yaml
   frontend:
     port: 8099
     host: 0.0.0.0
   ```

6. **Save** and **Start** the add-on

### 3. Enable MQTT Integration

The MQTT integration should auto-discover Zigbee2MQTT.

**If not automatic:**
1. **Go to**: Settings → Devices & Services
2. **Click**: "ADD INTEGRATION"
3. **Search**: "MQTT"
4. **Configure**:
   - Broker: `core-mosquitto` (or `192.168.0.166`)
   - Port: `1883`
   - Username/Password: (if configured)

### 4. Access Zigbee2MQTT Web UI

**URL**: http://192.168.0.166:8099

You should see the Zigbee2MQTT dashboard with:
- Coordinator information
- Device list (empty initially)
- "Permit Join" button to pair devices

---

## 📖 Detailed Setup

### Step 1: Check for Conflicts

**IMPORTANT**: Only ONE integration can use the Zigbee USB coordinator at a time.

#### Check if ZHA is Already Using the Device

1. **Go to**: Settings → Devices & Services
2. **Look for**: "Zigbee Home Automation" (ZHA)
3. **If ZHA exists**:
   - Click the three dots (⋮) on the ZHA card
   - Click "Delete"
   - Confirm deletion
   - Wait 30 seconds

#### Verify USB Device is Free

```bash
# In Terminal add-on
lsof /dev/ttyUSB0 2>/dev/null || echo "USB device is free"
```

If something is using it, you'll see the process name. Stop that process first.

---

### Step 2: Configure Zigbee2MQTT

#### Basic Configuration

**Settings → Add-ons → Zigbee2MQTT → Configuration**

```yaml
# Serial Configuration (REQUIRED)
serial:
  port: /dev/serial/by-id/usb-YOUR_DEVICE_ID_HERE
  adapter: auto  # or specific: zstack, deconz, ezsp
  baudrate: 115200

# MQTT Settings (usually auto-configured)
mqtt:
  server: mqtt://core-mosquitto:1883
  base_topic: zigbee2mqtt
  # Optional authentication
  # user: mqtt_user
  # password: !secret mqtt_password

# Frontend Settings
frontend:
  port: 8099
  host: 0.0.0.0
  # Optional authentication
  # auth_token: !secret zigbee2mqtt_auth_token

# Advanced Settings
advanced:
  # Zigbee Channel (11-26, avoid WiFi overlap)
  channel: 25

  # Network key (IMPORTANT: Generate unique key!)
  # Generate with: openssl rand -hex 16
  network_key: GENERATE

  # Pan ID (change if multiple Zigbee networks)
  pan_id: 6754

  # Log level
  log_level: info

# Home Assistant Integration
homeassistant: true

# Device Options
device_options:
  retain: true
  legacy: false

# Security: Disable permit join by default
permit_join: false

# Availability monitoring
availability: true
```

#### Generate Secure Network Key

**In Terminal add-on:**
```bash
openssl rand -hex 16
```

Example output: `a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6`

Update configuration:
```yaml
advanced:
  network_key: [0xa1, 0xb2, 0xc3, 0xd4, 0xe5, 0xf6, 0xg7, 0xh8, 0xi9, 0xj0, 0xk1, 0xl2, 0xm3, 0xn4, 0xo5, 0xp6]
```

---

### Step 3: Start Zigbee2MQTT

1. **Click**: "START" button
2. **Watch logs**: Click "Log" tab
3. **Look for success messages**:
   ```
   ✅ Zigbee2MQTT started
   ✅ Starting zigbee-herdsman
   ✅ Connected to MQTT server
   ✅ Started frontend on port 8099
   ✅ Zigbee: allowing new devices to join
   ```

4. **Verify web UI**: Open http://192.168.0.166:8099

---

## 🔍 Troubleshooting

### Issue: "Cannot lock port" Error

**Cause**: Another process (usually ZHA) is using the USB device.

**Solution**:
```bash
# Check what's using the device
lsof /dev/ttyUSB0

# If ZHA: Remove it from Settings → Devices & Services
# Then restart Zigbee2MQTT addon
```

See also: [ZIGBEE_PORT_LOCK_TROUBLESHOOTING.md](../../../Homelab_0925/services/home-automation/ZIGBEE_PORT_LOCK_TROUBLESHOOTING.md)

---

### Issue: "No such file or directory: /dev/ttyUSB0"

**Cause**: USB device not detected or path incorrect.

**Solution**:
```bash
# Find correct device path
ls -la /dev/serial/by-id/

# Update Zigbee2MQTT configuration with full path
# Example:
serial:
  port: /dev/serial/by-id/usb-Itead_Sonoff_Zigbee_3.0_USB_Dongle_Plus_V2_abc123-if00-port0
```

---

### Issue: Zigbee2MQTT Crashes on Startup

**Cause**: Wrong adapter type or corrupted configuration.

**Solution**:
```yaml
# Try specifying exact adapter type
serial:
  adapter: zstack  # For Sonoff, CC2652
  # adapter: deconz  # For ConBee
  # adapter: ezsp    # For HUSBZB-1
```

---

### Issue: Devices Not Appearing in Home Assistant

**Cause**: MQTT integration not configured or discovery disabled.

**Solution**:
1. Check MQTT integration exists (Settings → Devices & Services)
2. Verify `homeassistant: true` in Zigbee2MQTT config
3. Restart Home Assistant
4. Check MQTT integration shows Zigbee2MQTT bridge entity

---

## 📱 Device Pairing

### How to Pair Zigbee Devices

1. **Enable pairing mode**:
   - Open Zigbee2MQTT web UI: http://192.168.0.166:8099
   - Click "Permit Join (All)" button at top
   - Or run in Terminal: `mosquitto_pub -h localhost -t zigbee2mqtt/bridge/request/permit_join -m '{"value": true}'`

2. **Reset your Zigbee device**:
   - **Lights**: Turn on/off 5 times rapidly
   - **Sensors**: Hold reset button 5-10 seconds
   - **Switches**: Hold button until LED flashes
   - *(Check device manual for specific instructions)*

3. **Watch for device**:
   - Zigbee2MQTT logs will show: "Device joined"
   - Device appears in web UI device list
   - Device auto-discovers in Home Assistant

4. **Disable pairing** (for security):
   - Click "Permit Join" button again to disable
   - Or set `permit_join: false` in configuration

---

### Rename Devices

**In Zigbee2MQTT Web UI:**
1. Click on device in device list
2. Click "Settings" tab
3. Change "Friendly Name"
4. Device name updates in Home Assistant automatically

---

## 🤖 Integration with AI Voice Assistant

Once Zigbee devices are paired, they automatically work with your AI setup!

### Voice Command Examples

**With your AI voice assistant:**
- "Turn on the living room light"
- "Set bedroom temperature to 72 degrees"
- "What's the temperature in the kitchen?"
- "Turn off all lights"
- "Show me motion sensor status"

### Create AI Automations

**Example: AI-Controlled Lighting**
```yaml
# In automations.yaml
- alias: "AI Smart Lighting"
  trigger:
    - platform: conversation
      command:
        - "good night"
        - "bedtime"
  action:
    - service: script.smart_ai_router
      data:
        prompt: "It's bedtime. Please turn off all lights except the bedroom night light"
```

---

## 📊 Network Health Monitoring

### View Zigbee Network Map

**In Zigbee2MQTT Web UI:**
1. Click "Map" in top navigation
2. View visual representation of your Zigbee mesh
3. See which devices are:
   - **Coordinators** (red) - Your USB dongle
   - **Routers** (blue) - Powered devices (lights, plugs)
   - **End Devices** (yellow) - Battery devices (sensors)

### Check Device Signal Strength

1. Click device in device list
2. Check "Link Quality" value
3. **Good**: LQI > 100
4. **Fair**: LQI 50-100
5. **Poor**: LQI < 50 (consider adding router)

---

## 🔐 Security Best Practices

### 1. Generate Unique Network Key
```bash
openssl rand -hex 16
```
Never use default keys!

### 2. Disable Permit Join by Default
```yaml
permit_join: false
```
Only enable when actively pairing devices.

### 3. Enable Web UI Authentication
```yaml
frontend:
  auth_token: !secret zigbee2mqtt_auth_token
```

### 4. Use Stable Device Paths
```yaml
serial:
  port: /dev/serial/by-id/usb-YOUR-DEVICE-ID
  # Instead of /dev/ttyUSB0 which can change
```

---

## 🎯 Supported Devices

Zigbee2MQTT supports **3000+ devices** from major brands:

### Popular Device Categories
- **Lights**: Philips Hue, IKEA Tradfri, Sengled, Innr
- **Sensors**: Aqara, Sonoff, Third Reality, Tuya
- **Switches**: IKEA, Aqara, Tuya, Zemismart
- **Plugs**: Innr, Tuya, Third Reality, OSRAM
- **Thermostats**: Eurotronic, Danfoss, Tuya
- **Door Locks**: Yale, Danalock, Samsung
- **Blinds**: IKEA, Tuya, Zemismart

**Check compatibility**: https://www.zigbee2mqtt.io/supported-devices/

---

## 📚 Additional Resources

### Official Documentation
- **Zigbee2MQTT Docs**: https://www.zigbee2mqtt.io/
- **Device Database**: https://www.zigbee2mqtt.io/supported-devices/
- **Configuration Reference**: https://www.zigbee2mqtt.io/guide/configuration/

### Community
- **Zigbee2MQTT Discord**: https://discord.gg/dadfWYE
- **Home Assistant Community**: https://community.home-assistant.io/

---

## ✅ Success Checklist

- [ ] USB Zigbee coordinator connected
- [ ] Terminal & SSH add-on installed
- [ ] Checked for ZHA conflicts (removed if needed)
- [ ] Zigbee2MQTT add-on installed
- [ ] Serial port configured correctly
- [ ] Unique network key generated
- [ ] Add-on started successfully
- [ ] Web UI accessible (port 8099)
- [ ] MQTT integration configured
- [ ] First device paired successfully
- [ ] Device appears in Home Assistant
- [ ] Permit join disabled for security
- [ ] AI voice commands working with devices

---

**🎉 Congratulations!** You now have Zigbee device control integrated with your AI-powered Home Assistant setup!

Your voice assistants (Claude, ChatGPT, Gemini) can now control all your Zigbee devices. Try saying:
- "Turn on the lights"
- "What's the temperature?"
- "Set the thermostat to 72"

---

*Part of the [Home Assistant AI LAB](https://github.com/bibinabraham06/Home-Assistant-LAB) project*
*Version: 2.1.0 - Zigbee Integration*
