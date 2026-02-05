# Real-Time Multi-FX Pedal — Daisy Seed (DSP) + Raspberry Pi (Telemetry) + Godot UI

**Demo:** [link to video]  
**Tech:** C/C++, DaisySP/libDaisy, UART, Raspberry Pi OS (Linux), Python, JSON, Godot, Blender → Mixamo pipeline  
**Effects shipped:** Tuner, Chorus, Reverb, Bitcrusher/Distortion

## What this is
A two-processor embedded audio system: Daisy Seed handles real-time DSP, while a Raspberry Pi handles telemetry + system monitoring and drives a Godot UI. Daisy ↔ Pi communicate over UART. The UI displays effect parameters and system stats (CPU, temperature, Wi-Fi, footswitch) and shows a unique character per effect.

## Architecture (30-second overview)
- **Daisy Seed:** real-time audio callback pipeline + effects + control scanning
- **UART link:** compact line protocol for effect/params/switch + tuner data
- **Raspberry Pi:** Python daemon parses UART, writes `telemetry.json`
- **Godot UI:** reads telemetry and updates panels + character/scene state

![Architecture](docs/architecture.png)

## Features
- Real-time effects: tuner, chorus, reverb, bitcrusher/distortion
- Live telemetry: effect name/id, parameter values, timestamps, footswitch activity
- System diagnostics: CPU load, temperature, Wi-Fi status
- Effect-to-character mapping: Deadpool / Master Chief / Rei / Genji
- Analog front end: op-amp buffer + bias/coupling + grounding strategy (see docs)

## How to run (high level)
### Daisy firmware
1. [Build steps: toolchain + make]
2. Flash via DFU: [command]
3. UART output: [baud rate]

### Raspberry Pi telemetry
1. `cd pi && pip install -r requirements.txt`
2. `python telemetry_daemon.py`
3. Writes JSON to: `/dev/shm/pedal/telemetry.json` (or your path)

### Godot UI
1. Open `ui/` project in Godot
2. Set telemetry path (if configurable)
3. Run scene: [main scene]

## Protocol + Telemetry schema
- UART protocol: docs/uart_protocol.md
- JSON schema: docs/telemetry_schema.json

## Notes / Design decisions
- Why UART + JSON
- Why `/dev/shm` (low latency, avoids SD wear)
- Grounding/biasing notes for audio stability

## Future improvements
- [optional: list 3 next steps]
