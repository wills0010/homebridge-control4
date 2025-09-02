#DISCLAIMER

This software is neither affiliated with or endorsed by either Control4 or Apple.  

This SOFTWARE PRODUCT is provided "as is" and "with all faults." The developers make no representations
or warranties of any kind concerning the safety, suitability, lack of viruses, inaccuracies, typographical 
errors, or other harmful components of this SOFTWARE PRODUCT. There are inherent dangers in the use of any 
software, and you are solely responsible for determining whether this SOFTWARE PRODUCT is compatible with 
your equipment and other software installed on your equipment. You are also solely responsible for the 
protection of your equipment and backup of your data, and the developers will not be liable for any damages 
you may suffer in connection with using, modifying, or distributing this SOFTWARE PRODUCT. 

# Compatibility Note

In order for this plugin to function, you must have the Homebridge driver from Varietas Software installed
in your Control4 project. You can purchase it from <a href="https://www.houselogix.com/shop/homebridge-driver">HouseLogix</a>
or directly from <a href="http://www.varietassoftware.com/control4">Varietas Software</a>.  

# homebridge-control4

Supports bidirectional communication with a Control4 project on the HomeBridge Platform. Currently supports
native Control4 lights, dimmers, contact switches, garage door openers, ceiling fans (connected to switch),
fan speed controllers, blinds, motion sensors, locks, and security systems.

# Installation

1. Install homebridge using: npm install -g homebridge
2. Install homebridge-control4 using: npm install -g homebridge-control4
3. Update your configuration file. See sample-config.json in this repository for a sample. 

# Configuration

## Quick Start

**IMPORTANT:** You MUST change the `base_url` parameter to match your Control4 system!

Basic configuration sample:
```json
"accessories": [ 
{
  "accessory":"Control4",
  "name":"Kitchen Lights",
  "service":"Dimmer",
  "base_url":"http://YOUR_CONTROL4_IP:PORT/DEVICE_ID",
  "has_level_control":"yes",
  "switchHandling":"realtime",
  "brightnessHandling":"realtime",
  "refresh_interval":2000,
  "manufacturer":"Control4",
  "model":"ldz-102-w"
}
]
```

## Detailed Configuration Guide

For complete configuration instructions including all device types and options, see [CONFIGURATION.md](CONFIGURATION.md).

## What You Need to Change

1. **`base_url`** - Replace with your Control4 controller's IP, port, and device ID
   - Format: `http://[CONTROL4_IP]:[PORT]/[DEVICE_ID]`
   - Example: `http://192.168.1.201:8081/349`

2. **`name`** - Give your device a meaningful name

3. **`service`** - Set the device type: Switch, Light, Dimmer, Blinds, Thermostat, etc.

The configuration for compatible Control4 devices can be automatically output by the Varietas Software
Control4 homebridge driver. See documentation with that driver for details.

