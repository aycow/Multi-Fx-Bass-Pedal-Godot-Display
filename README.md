# Real-Time Multi-FX Pedal — Daisy Seed (DSP) + Raspberry Pi (Telemetry) + Godot UI

**Demo:** https://drive.google.com/file/d/1PNiA0a3cJR7EqutVgz4zbug7DsLo45Vx/view?usp=sharing
**Tech:** C/C++, DaisySP/libDaisy, UART, Raspberry Pi OS (Linux), Python, JSON, Godot, Blender → Mixamo pipeline  
**Effects shipped:** Tuner, Chorus, Reverb, Bitcrusher/Distortion

## What this is
A two-processor embedded audio system: Daisy Seed handles real-time DSP, while a Raspberry Pi handles telemetry + system monitoring and drives a Godot UI. Daisy ↔ Pi communicate over UART. The UI displays effect parameters and system stats (CPU, temperature, Wi-Fi, footswitch) and shows a unique character per effect.

## Architecture (30-second overview)
- **Daisy Seed:** real-time audio callback pipeline + effects + control scanning
- **UART link:** compact line protocol for effect/params/switch + tuner data
- **Raspberry Pi:** Python daemon parses UART, writes `telemetry.json`
- **Godot UI:** reads telemetry and updates panels + character/scene state

## Features
- Real-time effects: tuner, chorus, reverb, bitcrusher/distortion
- Live telemetry: effect name/id, parameter values, timestamps, footswitch activity
- System diagnostics: CPU load, temperature, Wi-Fi status
- Effect-to-character mapping: Deadpool / Master Chief / Eva / Genji
- Analog front end: op-amp buffer + bias/coupling + grounding strategy (see docs)

