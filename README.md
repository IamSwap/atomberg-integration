# Atomberg

[![GitHub Release][releases-shield]][releases]
[![GitHub Activity][commits-shield]][commits]
[![License][license-shield]](LICENSE)

![Project Maintenance][maintenance-shield]

[![Discord][discord-shield]][discord]
[![Community Forum][forum-shield]][forum]

*Home Assistant integration for **[Atomberg smart fans](https://atomberg.com/atomberg-ceiling-fans/smart-fans)** with **local control support***

## ✨ Features

- **🚀 Local Control**: Direct communication with fans for instant response (HTTP + UDP fallback)
- **☁️ Cloud Integration**: Full Atomberg cloud API support with automatic fallback
- **⚡ Real-time Updates**: UDP state broadcasts for immediate status updates  
- **🎛️ Full Device Control**: Fan speed, lighting, timers, sleep mode, and more
- **🔧 Advanced Features**: Brightness control and color effects for supported models (I1 series)
- **🏠 Home Assistant Integration**: Native entities for fans, lights, sensors, switches, and selects

## Tested on
- **[Atomberg Renesa+ Ceiling Fan](https://atomberg.com/atomberg-renesa-smart-iot-enabled-ceiling-fans-with-bldc-motor-and-remote)**
- **[Atomberg Aris Ceiling Fan](https://atomberg.com/aris-ceiling-fan)**
- **[Atomberg Erica Ceiling Fan](https://atomberg.com/erica-ceiling-fan)**

## Installation

### Method 1: Using HACS

1. Open your Home Assistant UI.
2. Go to "HACS" (Home Assistant Community Store).
3. Search for "Atomberg" in the search bar.
4. You should see the Atomberg integration listed.
5. Click "Install" and follow any prompts to complete the installation.

### Method 2: Manual Installation

1. Using the tool of choice open the directory (folder) for your HA configuration (where you find `configuration.yaml`).
2. If you do not have a `custom_components` directory (folder) there, you need to create it.
3. In the `custom_components` directory (folder) create a new folder called `atomberg`.
4. Download _all_ the files from the `custom_components/atomberg/` directory (folder) in this repository.
5. Place the files you downloaded in the new directory (folder) you created.
6. Restart Home Assistant.

## Configuration

### Step 1: Generate API Key and Refresh Token
1. Go to [Atomberg Developer Portal](https://developer.atomberg-iot.com/#overview).
2. Follow the instructions to generate your `api_key` and `refresh_token`.

### Step 2: Add Atomberg Integration to Home Assistant
1. Open your Home Assistant UI.
2. Navigate to "Configuration" -> "Integrations".
3. Click the "+" icon to add a new integration.
4. Search for "Atomberg" in the integration search bar and select it.

### Step 3: Configure Integration Settings
1. Enter your `api_key` and `refresh_token` in the appropriate fields.
2. **Enable Local Control** (recommended): Keep this checked for optimal performance and instant response times.
3. Submit the form.

#### Local Control Options
- **✅ Enabled (Default)**: Uses local HTTP/UDP communication for faster commands with cloud fallback
- **❌ Disabled**: Uses only cloud API communication (slower but works without local network access)

## 📋 Compatibility and Requirements

### Supported Devices
- **Latest Atomberg Smart Fans**: Designed for current-generation models
- **I1 Series**: Full feature support including brightness control and color effects
- **Older Models**: May have limited functionality

### Communication Methods
The integration uses a **hybrid approach** for optimal performance:

1. **🏠 Local HTTP Control** (Primary): Direct HTTP commands to device IP
2. **📡 Legacy UDP Control** (Fallback): Direct UDP commands to device IP  
3. **☁️ Cloud API** (Final Fallback): Commands via Atomberg cloud servers

### Network Requirements

#### Required Ports
- **UDP Port 5625** (Inbound): Device state broadcasts - **must be open on firewall**
- **HTTP Port 80** (Outbound): Local device control
- **UDP Port 5600** (Outbound): Legacy local control
- **HTTPS Port 443** (Outbound): Cloud API communication

#### Network Setup
- **Local Network**: Devices must be on the same network as Home Assistant for local control
- **Internet Access**: Required for initial setup and cloud API fallback
- **Firewall**: Ensure UDP port 5625 is not blocked

## 🚀 Performance & Benefits

### Local Control Advantages
- **⚡ Instant Response**: Commands execute immediately without cloud latency
- **🔄 Automatic Fallback**: Seamlessly switches to cloud if local communication fails  
- **📡 Real-time Updates**: UDP broadcasts provide immediate state synchronization
- **🌐 Works Offline**: Local control functions even when internet is unavailable
- **🔧 Smart Routing**: Integration automatically chooses the fastest available method

### Device Entities
The integration creates the following Home Assistant entities for each fan:

- **🌀 Fan Entity**: Speed control (1-6), power on/off
- **💡 Light Entity**: LED control with brightness and color temperature (I1 series)
- **🔄 Switch Entity**: Sleep mode toggle
- **⏰ Select Entity**: Timer control (Off, 1h, 2h, 3h, 6h)
- **📊 Sensor Entity**: Timer elapsed time with dynamic icons

## 🔧 Troubleshooting

### Local Control Issues
1. **Commands not working locally**:
   - Verify devices are on same network as Home Assistant
   - Check firewall settings for UDP port 5625
   - Try disabling and re-enabling local control in integration settings

2. **Slow response times**:
   - Enable local control if disabled
   - Check network connectivity between Home Assistant and fan devices
   - Monitor Home Assistant logs for connection issues

3. **Fan not discovered**:
   - Ensure API key and refresh token are correct
   - Verify fan is connected to Atomberg cloud via mobile app
   - Restart Home Assistant after fan setup

### Debug Logging
Add this to your `configuration.yaml` for detailed logging:
```yaml
logger:
  default: info
  logs:
    custom_components.atomberg: debug
```

## Contributions are welcome!

If you want to contribute to this please read the [Contribution guidelines](CONTRIBUTING.md)

## 📝 Changelog

### Version 2.0.0
- ✨ **NEW**: Local control support with HTTP API
- ✨ **NEW**: Multi-tier communication with intelligent fallback (HTTP → UDP → Cloud)
- ✨ **NEW**: Configuration option to enable/disable local control
- 🚀 **IMPROVED**: Faster response times with local communication
- 🚀 **IMPROVED**: Better reliability with multiple fallback methods
- 🔧 **IMPROVED**: Enhanced error handling and validation
- 🔧 **IMPROVED**: IP address validation for security
- 📝 **IMPROVED**: Comprehensive logging for troubleshooting

## Credits

- Code template was mainly taken from [@Ludeeus](https://github.com/ludeeus)'s [integration_blueprint][integration_blueprint] template
- Atomberg IoT Team for providing the device APIs and local control features
- Home Assistant community for feedback and testing


[integration_blueprint]: https://github.com/ludeeus/integration_blueprint
[commits-shield]: https://img.shields.io/github/commit-activity/y/dasshubham762/atomberg-integration.svg?style=for-the-badge
[commits]: https://github.com/dasshubham762/atomberg-integration/commits/main
[discord]: https://discord.gg/Qa5fW2R
[discord-shield]: https://img.shields.io/discord/330944238910963714.svg?style=for-the-badge
[forum-shield]: https://img.shields.io/badge/community-forum-brightgreen.svg?style=for-the-badge
[forum]: https://community.home-assistant.io/
[license-shield]: https://img.shields.io/github/license/dasshubham762/atomberg-integration.svg?style=for-the-badge
[maintenance-shield]: https://img.shields.io/badge/maintainer-%40dasshubham762-blue.svg?style=for-the-badge
[releases-shield]: https://img.shields.io/github/release/dasshubham762/atomberg-integration.svg?style=for-the-badge
[releases]: https://github.com/dasshubham762/atomberg-integration/releases
