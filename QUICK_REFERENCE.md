# Quick Configuration Reference

## What You MUST Change

### 1. base_url (REQUIRED)
```json
"base_url": "http://YOUR_CONTROL4_IP:PORT/DEVICE_ID"
```
**Examples:**
- `"base_url": "http://192.168.1.201:8081/349"`
- `"base_url": "http://192.168.6.9:8080/608"`

### 2. Device Name & Type (REQUIRED)
```json
"name": "Your Device Name",
"service": "Switch|Light|Dimmer|Blinds|Thermostat|Fan|etc"
```

## Device Types (service parameter)

| Service | Description | Use For |
|---------|-------------|---------|
| `Switch` | Basic on/off | Lights, outlets, etc. |
| `Light` | Light control | Non-dimmable lights |
| `Dimmer` | Dimmable light | Dimmable lights |
| `Blinds` | Window covering | Motorized blinds/shades |
| `Thermostat` | HVAC control | Temperature control |
| `Fan` | Fan with speed | Ceiling fans |
| `Garage Door` | Garage opener | Garage doors |
| `Lock` | Door lock | Electronic locks |
| `Contact` | Contact sensor | Door/window sensors |
| `Motion` | Motion sensor | Motion detectors |
| `Security` | Security system | Alarm panels |
| `Speaker` | Audio control | Speakers/zones |

## Common Optional Settings

```json
{
  "has_level_control": "yes",        // For dimmers/fans
  "switchHandling": "realtime",      // Real-time status updates
  "brightnessHandling": "realtime",  // Real-time brightness updates
  "refresh_interval": 2000,          // Update frequency (ms)
  "invert_contact": "no"             // For contact sensors
}
```

## Finding Your Control4 Information

1. **IP Address**: Check your Control4 controller's network settings
2. **Port**: Usually 8080, 8081, 8082 (check Control4 driver documentation)
3. **Device ID**: Provided by the Varietas Software Homebridge driver

## Testing Your Configuration

Try accessing this URL in a browser:
```
http://YOUR_CONTROL4_IP:PORT/DEVICE_ID/status
```
If it returns device status, your base_url is correct!

## Need More Help?

See [CONFIGURATION.md](CONFIGURATION.md) for complete detailed instructions.