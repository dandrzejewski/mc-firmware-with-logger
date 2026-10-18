# mc-firmware-with-logger

Mirrors upstream [MeshCore](https://github.com/meshcore-dev/MeshCore) repeater releases for the RAK3401 1W board (`RAK_3401_repeater`), built with packet logging enabled for use with [meshcoretomqtt](https://github.com/Cisien/meshcoretomqtt).

The only change from stock is one build-time flag, injected through `PLATFORMIO_BUILD_FLAGS`:

```
-D MESH_PACKET_LOGGING=1
```

No upstream source is copied or patched. Each run checks out the upstream release tag and builds it with upstream's own `build.sh`.

## Usage

1. Actions → **Build RAK3401 Repeater (packet logging)** → **Run workflow**.
2. Enter the upstream repeater version, e.g. `v1.18.0`. This builds upstream tag `repeater-v1.18.0`.
3. The firmware is published as a Release here with the same tag name as upstream (`repeater-v1.18.0`).

## Versioning

- Release tags match upstream repeater tags exactly.
- The device reports the same version string as the stock build (`v1.18.0-<upstream short sha>`).
- File names match upstream's, with a `-logging` suffix so they can't be mistaken for stock builds.
- Release notes link the upstream release and record the exact upstream commit.

## Output files

From upstream `build.sh` for nRF52 boards:

- `.uf2`: drag-and-drop flashing via the bootloader's USB drive
- `.zip`: DFU package
