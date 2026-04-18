<div align="center">

# 🏰 Yet Another HVAC Control Blueprint - But Different!

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/leboff/hass-blueprint-thermostat/refs/heads/main/hass-blueprint-thermostat.yaml)

![Home Assistant Logo](https://www.home-assistant.io/images/blog/2023-09-ha10/home-assistant-logo-new.png)

[![GitHub Stars](https://img.shields.io/github/stars/michaelheichler/hass-blueprint-thermostat?style=for-the-badge&logo=github)](https://github.com/michaelheichler/hass-blueprint-thermostat/stargazers)
[![GitHub Issues](https://img.shields.io/github/issues/michaelheichler/hass-blueprint-thermostat?style=for-the-badge&logo=github)](https://github.com/michaelheichler/hass-blueprint-thermostat/issues)
[![Buy me a coffee](https://img.shields.io/badge/PayPal-Buy%20me%20a%20coffee-blue?style=for-the-badge&logo=paypal)](https://paypal.me/MHeichler)

</div>

## 🎯 Overview

An intelligent Home Assistant blueprint for HVAC control that goes beyond simple window-open detection. This blueprint focuses on energy efficiency while maintaining comfort through smart temperature management and configurable behaviors.

## 🆕 What's New

- **Multi-zone HVAC support (area-based).** Provide multiple climate entities via `climate_entities`. When a window opens, the blueprint looks up that window's Home Assistant area and only turns off climate entities in the same area. Restoration only fires once every window in that zone is closed.
- **`zone_mode` setting.** Choose `area` (true zoning by HA area) or `shared` (all listed climates are treated as one pool - legacy behavior).
- **Backward compatible.** The legacy `climate_entity` input is still accepted and is merged into the multi-zone list; existing automations keep working without reconfiguration.
- **Bug fixes.**
  - `any_window_open` now correctly reports whether any window is open (previous template always returned `false`).
  - State restoration now calls `climate.turn_on` so HA restores the prior mode, instead of reading the mode *after* turn-on.
  - Notifications, area names, and reminders use the triggering window's area and friendly name rather than always `window_sensors[0]`.
  - `seasonal_mode` now actually gates the HVAC-off action.
  - `require_temperature_sensor` is enforced as a top-level condition.
  - `debug_mode` writes to the HA logbook at key decision points.
  - Daytime/nighttime handling merged into a single sequence with a templated delay.
  - Entity-list `state: "on"` conditions replaced with templates so "any" (not "all") is correctly evaluated.
  - Timer-duration display no longer breaks on durations that include hours.
- **Optional notification throttle helper.** Point `notification_throttle_store` at an `input_datetime` and the cooldown becomes functional; leave it blank to skip.
- **Fahrenheit support.** New `temperature_unit` input (`°C` or `°F`). Thresholds are entered in the chosen unit and notifications display it. If the outdoor temperature sensor reports a different unit than you selected, its value is converted automatically using the sensor's `unit_of_measurement` attribute.

## ✨ Key Features

- 🌡️ **Smart Temperature Thresholds**
  - Intelligent HVAC control based on outdoor temperature
  - Configurable high/low temperature thresholds

- ⏰ **Time-Aware Operation**
  - Different behaviors for day and night
  - Customizable timeouts for both periods
  - Evening checks for open windows before bedtime

- 🔄 **Intelligent State Management**
  - Remembers previous HVAC modes
  - Smart restoration after window closure
  - Prevents unnecessary system cycling

- 📊 **Environmental Monitoring**
  - Optional humidity monitoring
  - Atmospheric pressure tracking
  - Temperature-based decisions

- 📱 **Smart Notifications**
  - Detailed status updates
  - Window location information
  - Customizable notification cooldowns

## 🛠️ Installation

1. Click the "Import Blueprint" button above
2. Configure the following required entities:
   - Climate entity (your HVAC system)
   - Window/door sensors
   - Notification device
3. Optional: Add environmental sensors
   - Temperature sensor
   - Humidity sensor
   - Pressure sensor
4. Set your preferred thresholds and timings

## ⚙️ Configuration Options

### Required Settings
- `climate_entities`: One or more HVAC systems (multi-zone); legacy `climate_entity` still accepted
- `zone_mode`: `area` (default) or `shared` - see "What's New" above
- `window_sensors`: Window/door sensors to monitor (assign areas for zoning)
- `notify_device`: Device for notifications

### Optional Settings
- `temperature_sensor`: Outdoor temperature monitoring
- `humidity_sensor`: Humidity monitoring
- `pressure_sensor`: Atmospheric pressure monitoring
- `seasonal_mode`: Summer/Winter/Auto operation modes
- `restore_climate_state`: Remember previous HVAC states

### Timing Configuration
- `daytime_hvac_timeout`: Delay before HVAC shutdown during day
- `nighttime_hvac_timeout`: Delay before HVAC shutdown at night
- `night_check_time`: Time for evening window checks
- `notification_cooldown`: Minimum time between notifications

## 🔮 Roadmap

- [ ] Indoor humidity monitoring and ventilation reminders
- [ ] Weather forecast integration for rain warnings
- [ ] Advanced door security checks for night time
- [ ] Extended seasonal operation modes
- [ ] Smart home system integrations
- [x] Multi-zone HVAC support (area-based)
- [ ] Energy consumption analytics
- [ ] Custom notification templates

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👨‍💻 About the Author

Created by Michael Heichler, a Data Scientist specializing in AI and automation. Passionate about creating smart home solutions that combine energy efficiency with practical automation.

Got questions or suggestions? Feel free to:
- Open an issue
- Start a discussion
- Send me a PM on the Home Assistant forum

## ☕ Support

If you find this blueprint helpful, consider supporting the development:

[!["Buy Me A Coffee"](https://img.shields.io/badge/PayPal-Buy%20me%20a%20coffee-blue?style=for-the-badge&logo=paypal)](https://paypal.me/MHeichler)

## 📊 Stats

![GitHub Stars](https://img.shields.io/github/stars/michaelheichler/hass-blueprint-thermostat?style=for-the-badge&logo=github)
![GitHub Issues](https://img.shields.io/github/issues/michaelheichler/hass-blueprint-thermostat?style=for-the-badge&logo=github)
![GitHub Last Commit](https://img.shields.io/github/last-commit/michaelheichler/hass-blueprint-thermostat?style=for-the-badge&logo=github)

---

<div align="center">
Made with ❤️ for the Home Assistant Community
</div>
