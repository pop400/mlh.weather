# My Weather (mlh.weather)

An Omarchy shell bar-widget plugin: a weather pill on the bar with a detail
popup. Forked from Omarchy's stock `omarchy.weather` plugin, with two changes:

- The detail popup's forecast row shows **5 days, including today** (the
  stock plugin only shows upcoming days).
- **Click any day tile** (today included) to expand an **hourly breakdown**
  for that day, sourced from the Open-Meteo API.

## Requirements

- [Omarchy](https://omarchy.org) with its Quickshell-based bar/shell.
- `curl` on `PATH` (used for both weather data and geocoding lookups).
- Internet access to `wttr.in`, `api.open-meteo.com`, and
  `geocoding-api.open-meteo.com`.

## Setup

1. Copy this folder into your Omarchy plugins directory, keeping the folder
   name as the plugin id:

   ```sh
   git clone <this-repo-url> ~/.config/omarchy/plugins/mlh.weather
   ```

2. Enable the plugin and add it to the bar. Either:
   - Run `omarchy plugin enable mlh.weather` (or use the Omarchy settings UI
     to add the "My Weather" bar widget under the Info category), or
   - If you're replacing the stock weather widget, disable
     `omarchy.weather` first so only one weather pill shows.

3. Reload the shell so the new plugin is picked up:

   ```sh
   omarchy restart shell
   ```

4. Click the weather pill to open the detail popup, then click the location
   label and search for your city. Selecting a result geocodes it via
   Open-Meteo and saves it to
   `~/.local/state/omarchy/settings/weather.json` — no manual config file
   editing needed. Without a saved location, the plugin falls back to
   wttr.in's IP-based lookup (current conditions only, no hourly data).

5. Click any tile in the 5-day forecast row (including "Today") to expand
   its hourly forecast; click it again to collapse.

## Notes

- Temperature units follow the `unit` setting exposed in the plugin's
  settings form, falling back to your locale/country when unset.
- The hourly breakdown is only available when a location has been searched
  and saved (i.e. Open-Meteo coordinates are known) — the wttr.in fallback
  path has no hourly data.
