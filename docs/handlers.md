# Built-in Handlers

The plugin automatically applies the following settings on `ApplySettings()`:

## Display (bEnableDisplayHandlers)

| Setting Id | Action |
|-----------|--------|
| DisplayMode | `UGameUserSettings::SetFullscreenMode` |
| Resolution | `UGameUserSettings::SetScreenResolution` (dynamic options) |
| ResolutionScale | cvar `r.ScreenPercentage` |
| VSync | `UGameUserSettings::SetVSyncEnabled` |
| FrameRateLimit | `UGameUserSettings::SetFrameRateLimit` (0/30/60/90/120/144/165/240) |
| Brightness | `GEngine->DisplayGamma` |

## Scalability (bEnableScalabilityHandlers)

| Setting Id | Action |
|-----------|--------|
| OverallQuality | Sets all individual qualities (0=Low, 1=Med, 2=High, 3=Epic, 4=Custom) |
| TextureQuality, ShadowQuality, EffectsQuality, PostProcessQuality, AntiAliasingQuality, ViewDistanceQuality, FoliageQuality, ShadingQuality, GlobalIlluminationQuality, ReflectionQuality | Scalability system (0-3) |

## Post-Process (bEnablePostProcessHandlers)

| Setting Id | cvar | On / Off |
|-----------|------|----------|
| MotionBlur | `r.MotionBlurQuality` | 4 / 0 |
| ChromaticAberration | `r.SceneColorFringe.Max` | 100 / 0 |
| FilmGrain | `r.FilmGrain` | 1 / 0 |
| Bloom | `r.BloomQuality` | 5 / 0 |

## Upscaler (bEnableUpscalerHandlers)

| Setting Id | Action |
|-----------|--------|
| UpscaleMethod | Switching None/FXAA/TAA/TSR/DLSS/FSR |
| ResolutionScale | cvar `r.ScreenPercentage` |

The plugin provides basic upscaler integration: auto-detects available DLSS/FSR at startup, builds option list, and switches between them. DLSS and FSR plugins are **not included** -- install them separately (NVIDIA DLSS Plugin, AMD FSR Plugin).

This covers the typical settings menu scenario. If your project needs deeper upscaler configuration (Quality/Balanced/Performance presets, sharpness, etc.), implement your own logic by disabling `bEnableUpscalerHandlers` and subscribing to `OnSettingsApplied`.

## Audio Device (bEnableAudioDeviceManagement)

| Setting Id | Action |
|-----------|--------|
| AudioOutputDevice | Switch output device (dynamic options) |

## Game Settings (FOV, volume, sensitivity, etc.)

These settings are handled on the game side, as their application depends on the specific project. Subscribe to `OnSettingsApplied` and read values from the manager. Working implementation example -- `BP_SettingsCharacter` in `Example/Blueprints/`.

## Handler Toggle System

Each built-in logic block can be disabled in Project Settings -> Handlers.

When a handler is disabled:
- The setting still saves/loads
- `OnSettingChanged` still fires
- Built-in logic (cvars, UGameUserSettings) **is not called**

This allows replacing any block with your own implementation by subscribing to `OnSettingsApplied`.
