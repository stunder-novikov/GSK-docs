# Project Settings

Project Settings -> Plugins -> Game Settings Kit

| Section | Setting | Description |
|---------|---------|-------------|
| Settings Data | Settings Data Assets | Array of references to Data Assets with settings |
| Key Bindings | Key Bindings Data Assets | Array of references to Data Assets with key binding contexts |
| Categories | Categories | List of categories (default: Display, Graphics, Audio, Input, Gameplay). Add your own. |
| General | Run Benchmark On First Launch | Run the hardware benchmark the first time the game starts, outside the editor (true). See [Hardware Benchmark](docs/api-benchmark.md) |
| Handlers | bEnableDisplayHandlers | Built-in display handlers (true) |
| Handlers | bEnableScalabilityHandlers | Built-in scalability handlers (true) |
| Handlers | bEnablePostProcessHandlers | Built-in post-process handlers (true) |
| Handlers | bEnableUpscalerHandlers | Built-in upscaler handlers (true) |
| Handlers | bEnableAudioDeviceManagement | Built-in audio device management (true) |
| Defaults | Reset Data Assets to Defaults (button) | Replaces both Data Asset lists with the plugin's example Data Assets |

The first time the editor opens a project that configures no Data Assets, Game Settings Kit fills both lists with its example Data Assets and saves them in your project's `Config/DefaultGameSettingsKit.ini`. Commit that file. After that, whatever you remove, replace or empty stays as you left it. Use **Reset Data Assets to Defaults** to get the examples back.

A project that already lists its own Data Assets keeps them, including projects upgraded from 1.0.0. Packaged games, dedicated servers and commandlets never write this file.
