# Fork changes

This is a personal fork of [cleyton1986/predator-sense](https://github.com/cleyton1986/predator-sense)
(GPL-3.0), based on `v0.3.14-preview` (`bd3d75d`). All credit for the project
goes to its original author, Cleyton Alves. This file lists only what differs
from upstream.

Tested on one machine: Acer Predator Helios Neo 16 **PHN16-71**, Kali Linux,
kernel 7.1.5, KDE Plasma on Wayland.

## Changes

| Date | Commit | Change |
|---|---|---|
| 2026-11-03 | `1d07d5c` | `auto_profile_ac` is off by default. Plugging in the charger no longer switches a user who picked Balanced to Performance. |
| 2026-11-03 | `e22acf1` | The hotkey service looks for a `wayland-N` socket in `XDG_RUNTIME_DIR` when it starts without `DISPLAY` or `WAYLAND_DISPLAY`, instead of guessing `DISPLAY=:0`. |
| 2026-11-03 | `29d2816` | The software fan curve smooths the temperature it answers to. Rising moves 30% of the way per tick, falling 50%, and 85 C or more is used as it is. A one-second CPU boost no longer ramps the fans. |
| 2026-11-03 | `2d939d8` | The PredatorSense key is recognised on the PHN16-71, which reports it as `KEY_PROG1` (148) instead of 425. Other models are unchanged. |

## What has been verified

| Change | Automated tests | On the PHN16-71 |
|---|---|---|
| Hotkey: PHN16-71 key code | yes | **Yes**: the key opens the app, started by the hotkey daemon |
| Hotkey: Wayland socket | yes | Not shown separately from the key code |
| AC profile default | yes | Config reads `auto_profile_ac: false`; charger plug/unplug not tried |
| Fan temperature smoothing | yes | Not tried; it only applies with Auto curve switched on |

## Not changed

- The `facer` kernel module. Fan PWM control and Turbo are untested on this
  model, and upstream has an open report of a Turbo shutdown on a related one
  (cleyton1986/predator-sense#97). Avoid Turbo.
- Everything else is as upstream.

## Building and installing this fork

```bash
cd predator-sense-gui
cargo build --release
cargo build --release --manifest-path installer/Cargo.toml
sudo installer/target/release/predator-sense-installer --install
```

Run the installer from this build, not the one from the upstream releases page,
or upstream's binaries are installed instead. Reboot afterwards.

## License

GPL-3.0, as upstream. See `LICENSE`.
