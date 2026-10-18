# mc-firmware-with-logger

Builds unmodified upstream [MeshCore](https://github.com/meshcore-dev/MeshCore) repeater firmware for the RAK3401 1W board (`RAK_3401_repeater`) with packet logging enabled, for use with [meshcoretomqtt](https://github.com/Cisien/meshcoretomqtt).

The only change from stock is one build-time flag, injected through `PLATFORMIO_BUILD_FLAGS`:

```
-D MESH_PACKET_LOGGING=1
```

No upstream source is copied or patched. Each run checks out `meshcore-dev/MeshCore` at the requested ref and builds it with upstream's own `build.sh`.

## Usage

1. Actions → **Build RAK3401 Observer Repeater** → **Run workflow**.
2. Enter an upstream ref: a release tag (e.g. `repeater-v1.14.1`), a branch (`main`), or a commit SHA.
3. When the run finishes, the firmware is attached to a new Release named after the version and upstream commit.

Release tags follow `rak3401-observer-<version>-<upstream short sha>`. The release notes record the exact upstream ref, commit, and extra build flags.

## Output files

From upstream `build.sh` for nRF52 boards:

- `.uf2`: drag-and-drop flashing via the bootloader's USB drive
- `.zip`: DFU package
