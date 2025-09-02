# Homebridge Control4 Configuration Guide

This guide explains what configuration parameters need to be changed when setting up the homebridge-control4 plugin.

## Required Configuration Changes

### 1. Base URL (`base_url`)

**Most Important Parameter** - This is the primary configuration that must be changed for your specific Control4 system.

```json
"base_url": "http://192.168.1.201:8081/349"
```

**Format:** `http://[CONTROL4_IP]:[PORT]/[DEVICE_ID]`

- `CONTROL4_IP`: IP address of your Control4 controller
- `PORT`: Port number (typically 8080, 8081, etc.)
- `DEVICE_ID`: Unique identifier for the specific device/room

**Examples:**
```json
"base_url": "http://192.168.6.9:8080/608"     // Blinds device
"base_url": "http://192.168.1.100:8081/123"   // Light device
"base_url": "http://10.0.1.50:8082/456"       // Thermostat device
```

### 2. Device Information

**Required:**
```json
{
  "accessory": "Control4",
  "name": "Your Device Name",
  "service": "Switch|Light|Dimmer|Blinds|Thermostat|etc",
  "base_url": "http://YOUR_CONTROL4_IP:PORT/DEVICE_ID"
}
```

**Service Types Available:**
- `Switch` - Basic on/off control
- `Light` - Light control (on/off)
- `Dimmer` - Dimmable light (on/off + brightness)
- `Blinds` - Window covering control
- `Thermostat` - HVAC control
- `Fan` - Fan control with speed
- `Garage Door` - Garage door opener
- `Lock` - Door lock control
- `Contact` - Contact sensor
- `Motion` - Motion sensor
- `Security` - Security system
- `Speaker` - Audio control
- `Doorbell` - Doorbell sensor
- `Keypad` - Multi-button keypad

### 3. Network Configuration

The plugin automatically configures network settings based on your `base_url`:

**Automatic Port Calculation:**
```javascript
// Port is calculated as: last part of base_url + 10000
// Example: base_url ends with "/349" → port = 349 + 10000 = 10349
```

**IP Detection:**
The plugin automatically detects your local IP and notifies the Control4 system.

### 4. Device-Specific Options

#### For Dimmers/Lights:
```json
{
  "has_level_control": "yes",
  "brightnessHandling": "realtime",
  "switchHandling": "realtime"
}
```

#### For Contact Sensors:
```json
{
  "invert_contact": "no"  // Set to "yes" if sensor logic is inverted
}
```

#### For Thermostats:
```json
{
  "cool_string": "Cool",
  "heat_string": "Heat", 
  "off_string": "Off",
  "auto_string": "Auto"
}
```

#### For Security Systems:
```json
{
  "has_on_state": "yes",
  "has_power_control": "no"
}
```

### 5. Polling Configuration

```json
{
  "refresh_interval": 2000,        // Milliseconds between status checks
  "switchHandling": "realtime",    // "realtime" or "no"
  "brightnessHandling": "realtime" // "realtime" or "no"
}
```

### 6. Device Metadata (Optional)

```json
{
  "manufacturer": "Control4",
  "model": "ldz-102-w",
  "serial": "Your-Serial-Number"
}
```

## Complete Configuration Examples

### Light/Dimmer:
```json
{
  "accessory": "Control4",
  "name": "Kitchen Lights",
  "service": "Dimmer",
  "base_url": "http://192.168.1.201:8081/349",
  "has_level_control": "yes",
  "switchHandling": "realtime",
  "brightnessHandling": "realtime",
  "refresh_interval": 2000,
  "manufacturer": "Control4",
  "model": "ldz-102-w"
}
```

### Blinds:
```json
{
  "accessory": "Control4",
  "name": "Master Blinds",
  "service": "Blinds",
  "base_url": "http://192.168.6.9:8080/608",
  "switchHandling": "realtime",
  "refresh_interval": 900000,
  "manufacturer": "Control4",
  "model": "Blinds"
}
```

### Thermostat:
```json
{
  "accessory": "Control4",
  "name": "Main Floor Thermostat",
  "service": "Thermostat",
  "base_url": "http://192.168.1.201:8081/500",
  "cool_string": "Cool",
  "heat_string": "Heat",
  "off_string": "Off",
  "auto_string": "Auto",
  "refresh_interval": 30000
}
```

## What URLs are Built from base_url

The plugin automatically constructs these endpoint URLs:

### Control URLs:
- `{base_url}/on` - Turn device on
- `{base_url}/off` - Turn device off  
- `{base_url}/level/{brightness}` - Set brightness level
- `{base_url}/set_blinds_target/{position}` - Set blind position

### Status URLs:
- `{base_url}/light_state` - Get light status
- `{base_url}/contact_state` - Get contact/motion status
- `{base_url}/brightness` - Get brightness level
- `{base_url}/blinds_level` - Get blind position
- `{base_url}/blinds_target` - Get blind target position

### Thermostat URLs:
- `{base_url}/hvac_mode` - Get HVAC mode
- `{base_url}/hvac_status` - Get HVAC status
- `{base_url}/temperature` - Get current temperature
- `{base_url}/heat_setpoint` - Get heat setpoint
- `{base_url}/cool_setpoint` - Get cool setpoint
- `{base_url}/set_hvac_mode/{mode}` - Set HVAC mode
- `{base_url}/set_heat_setpoint/{temp}` - Set heat setpoint
- `{base_url}/set_cool_setpoint/{temp}` - Set cool setpoint

## Authentication (If Required)

```json
{
  "username": "your_username",
  "password": "your_password",
  "sendimmediately": true
}
```

## Troubleshooting

1. **Check base_url format** - Must include http:// and be reachable from your Homebridge system
2. **Verify device ID** - The number at the end of base_url must match your Control4 device
3. **Test connectivity** - Ensure you can access `http://YOUR_CONTROL4_IP:PORT/DEVICE_ID/status` in a browser
4. **Check Control4 driver** - Ensure the Varietas Software Homebridge driver is installed in your Control4 project

## Summary of Required Changes

**At minimum, you MUST change:**
1. `base_url` - Point to your Control4 system and device
2. `name` - Give your device a meaningful name
3. `service` - Match the type of Control4 device

**Commonly changed:**
- `refresh_interval` - Adjust polling frequency
- `switchHandling`/`brightnessHandling` - Enable real-time updates
- Device-specific options based on your hardware

**Optional:**
- Authentication credentials
- Manufacturer/model information
- Advanced device-specific settings