# Built-in Handlers

The plugin applies the following settings at startup (saved values) and on every `ApplySettings()`:

## Display (bEnableDisplayHandlers)

| Setting Id | Action |
|-----------|--------|
| DisplayMode | `UGameUserSettings::SetFullscreenMode` |
| Resolution | `UGameUserSettings::SetScreenResolution` (dynamic options; saved as e.g. `1920x1080`, see [Dynamic Enum Options](docs/api-dynamic.md)) |
| VSync | `UGameUserSettings::SetVSyncEnabled` |
| FrameRateLimit | `UGameUserSettings::SetFrameRateLimit` (0/30/60/90/120/144/165/240) |
| Brightness | `GEngine->DisplayGamma` |

At startup, the command-line options `-ResX`, `-ResY`, `-Res=`, `-Windowed` and `-FullScreen` win over the saved display mode and resolution. The saved values are kept, and the first Apply from the menu uses the player's values again.

## Scalability (bEnableScalabilityHandlers)

| Setting Id | Action |
|-----------|--------|
| OverallQuality | Sets all individual qualities (0=Low, 1=Med, 2=High, 3=Epic, 4=Custom). A saved value with no matching option loads as Custom. |
| TextureQuality, ShadowQuality, EffectsQuality, PostProcessQuality, AntiAliasingQuality, ViewDistanceQuality, FoliageQuality, ShadingQuality, GlobalIlluminationQuality, ReflectionQuality | Scalability system (0-3) |

A saved value of any Enum setting that matches none of its options (hand-edited, or the option list changed) is replaced by the setting's default when loaded, and a line is logged.

## Post-Process (bEnablePostProcessHandlers)

| Setting Id | cvar | On | Off |
|-----------|------|----|-----|
| MotionBlur | `r.MotionBlurQuality` | follows the quality level | 0 |
| ChromaticAberration | `r.SceneColorFringe.Max` | follows the quality level | 0 |
| FilmGrain | `r.FilmGrain` | follows the quality level | 0 |
| Bloom | `r.BloomQuality` | follows the quality level | 0 |

"On" uses the value of the current scalability level (or the engine default). For example, motion blur on at Low quality stays off, as the engine's Low level has it. "Off" holds the effect at 0 through quality changes.

These values, and Resolution Scale, are held at scalability priority. If your project sets one of these console variables at a higher priority (`[SystemSettings]` in DefaultEngine.ini, ConsoleVariables.ini, a device profile, the command line or a console command), the project's value wins, and the manager logs this once. Writing `sg.*` directly or switching device profiles at run time overrides an effect switched off until the next quality change or Apply.

## Upscaler (bEnableUpscalerHandlers)

| Setting Id | Action |
|-----------|--------|
| UpscaleMethod | Switching None/FXAA/TAA/TSR/DLSS/FSR |
| ResolutionScale | cvar `r.ScreenPercentage` (held at scalability priority, see above) |

The plugin provides basic upscaler integration: at startup it checks whether the DLSS and FSR plugins are enabled, builds the option list, and switches between them. It detects the plugins, not GPU support. DLSS and FSR plugins are **not included** -- install them separately (NVIDIA DLSS Plugin, AMD FSR Plugin).

The choice is saved by name (`TSR`, `DLSS`, `FSR`). If a build no longer contains the saved upscaler, TSR is used.

This covers the typical settings menu scenario. If your project needs deeper upscaler configuration (Quality/Balanced/Performance presets, sharpness, etc.), implement your own logic by disabling `bEnableUpscalerHandlers` and subscribing to `OnSettingsApplied`.

## Audio Device (bEnableAudioDeviceManagement)

| Setting Id | Action |
|-----------|--------|
| AudioOutputDevice | Switch output device (dynamic options; saved by device id) |

The device is switched only when the player picks one other than the device in use, so repeated Apply calls do not interrupt audio. If the engine moves the output by itself (the device is unplugged, or the system default changes), the next Apply restores the player's choice.

## Game Settings (FOV, volume, sensitivity, etc.)

These settings are handled on the game side, as their application depends on the specific project. Subscribe to `OnSettingsApplied` and read values from the manager. Working implementation example -- `BP_SettingsCharacter` and `BP_SettingsPC` in `/GameSettingsKit/Example/Blueprints/`.

## Handler Toggle System

Each built-in logic block can be disabled in Project Settings -> Handlers.

When a handler is disabled:
- The setting still saves/loads
- `OnSettingChanged` still fires
- Built-in logic (cvars, UGameUserSettings) **is not called**

This allows replacing any block with your own implementation by subscribing to `OnSettingsApplied`.

## Play In Editor

Settings applied during Play In Editor change the editor's own process. When PIE ends, the editor gets back its console variables, scalability levels, display gamma and its saved game user settings. The player's values stay saved and apply again in the next PIE session. The hardware benchmark never runs in the editor.
