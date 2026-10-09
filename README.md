# Game Settings Kit

**Production-ready game settings system for Unreal Engine 5.7 and 5.8.**

Data-driven architecture: settings defined in Data Assets, UI built in Blueprint, all apply logic in C++ core.

## Features

- Display, Graphics, Audio, Input, Gameplay settings
- Upscaler switching (TSR / TAA / FXAA, plus DLSS and FSR when their plugins are enabled)
- Audio output device management with hot-plug
- Key remapping via Enhanced Input
- Resolution confirmation dialog: reverts unconfirmed changes after a countdown, also while the game is paused
- Hardware auto-detect on first launch (optional)
- Overall Quality sync with individual settings
- Persistence in GameUserSettings.ini (resolution and upscaler saved by name, so saves survive hardware and build changes)
- Handler toggle system -- disable any built-in logic
- Custom categories via Project Settings
- Full C++ and Blueprint API

## Getting Started

See [Quick Start](docs/quickstart.md) and [Integration Guide](docs/integration.md).

Get it on Fab: https://www.fab.com/listings/9d2305f7-1e80-476a-b299-123190a1ee73

Upgrading from 1.0.0? Read the [Changelog](docs/changelog.md) first.
