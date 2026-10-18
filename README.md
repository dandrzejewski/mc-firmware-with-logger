# mc-firmware-with-logger

Mirrors upstream [MeshCore](https://github.com/meshcore-dev/MeshCore) repeater releases, built with packet logging enabled for use with [meshcoretomqtt](https://github.com/Cisien/meshcoretomqtt).

The only change from stock is one build-time flag, injected through `PLATFORMIO_BUILD_FLAGS`:

```
-D MESH_PACKET_LOGGING=1
```

No upstream source is copied or patched. Each run checks out the upstream release tag and builds it with upstream's own `build.sh`.

## Boards

| Board | Upstream env | Platform |
|---|---|---|
| RAK3401 1W | `RAK_3401_repeater` | nRF52 |
| RAK4631 | `RAK_4631_repeater` | nRF52 |
| Heltec V4 (OLED) | `heltec_v4_repeater` | ESP32 |
| Heltec Wireless Tracker V2 | `heltec_tracker_v2_repeater` | ESP32 |
| Heltec Mesh Node T096 | `Heltec_t096_repeater` | nRF52 |
| Heltec Mesh Node T114 | `Heltec_t114_repeater` | nRF52 |
| Seeed Wio Tracker L1 | `WioTrackerL1_repeater` | nRF52 |
| Seeed Wio Tracker L1 1W | `WioTrackerL1-1W_repeater` | nRF52 |

To add a board, append its upstream env name to `PIO_ENVS` in the workflow and add a row to this table. All boards build in one job, so if any board fails, nothing is published.

## Usage

1. Actions → **Build Repeater Firmware (packet logging)** → **Run workflow**.
2. Enter the upstream repeater version, e.g. `v1.18.0`. This builds upstream tag `repeater-v1.18.0`.
3. The firmware for every board is published as a single Release here with the same tag name as upstream (`repeater-v1.18.0`).

## Versioning

- Release tags match upstream repeater tags exactly.
- The device reports the same version string as the stock build (`v1.18.0-<upstream short sha>`).
- File names match upstream's, with a `-logging` suffix so they can't be mistaken for stock builds.
- Release notes link the upstream release, record the exact upstream commit, and list the envs built.

## Output files

From upstream `build.sh`, depending on platform:

- nRF52 `.uf2`: drag-and-drop flashing via the bootloader's USB drive
- nRF52 `.zip`: DFU package
- ESP32 `-merged-logging.bin`: full image (bootloader, partitions, app) for a fresh flash at offset `0x0`
- ESP32 `-logging.bin`: app-only image for updating a board that already runs MeshCore
