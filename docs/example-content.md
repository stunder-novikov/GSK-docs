# Example Content

The plugin includes a working example in `/GameSettingsKit/Example/` (Content Browser: Plugins > Game Settings Kit Content > Example; enable Show Plugin Content). Open `Maps/L_SettingsExample` and press Play, then Escape.

## Data Assets

| Asset | Description |
|-------|-------------|
| DA_DisplaySettings | Display mode, resolution, VSync, FPS limit, brightness, FOV, resolution scale |
| DA_GraphicsSettings | Overall Quality, 7 individual qualities (texture, shadow, effects, post processing, anti-aliasing, view distance, foliage), post-process toggles, upscaler |
| DA_AudioSettings | 5 volume sliders + output device |
| DA_InputSettings | Mouse sensitivity, ADS sensitivity, invert Y |
| DA_GameplaySettings | HUD scale, FPS counter, crouch/sprint/ADS modes |
| DA_KeyBindings | References IMC_Example |

## Widgets

| Widget | Parent | Purpose |
|--------|--------|---------|
| WBP_SettingsMenu | GSKSettingsWidget | Settings menu with category tabs |
| WBP_SettingRow_Bool | GSKSettingRowWidget | Checkbox row |
| WBP_SettingRow_Slider | GSKSettingRowWidget | Slider row |
| WBP_SettingRow_Enum | GSKSettingRowWidget | Dropdown row |
| WBP_SettingRow_Key | UserWidget | Key binding row |
| WBP_CaptureOverlay | UserWidget | Overlay for capturing any key/mouse input |
| WBP_ResolutionConfirm | GSKResolutionConfirmWidget | Resolution confirmation dialog |

## Other assets

| Folder | Assets | Purpose |
|--------|--------|---------|
| Maps | L_SettingsExample | Example level |
| Blueprints | GM_Settings, BP_SettingsPC, BP_SettingsCharacter, WBP_SettingsHud | Game mode; player controller (Escape opens the menu, applies volumes with Set Sound Class Volume); character applying FOV/sensitivity/modes on OnSettingsApplied; HUD |
| Audio | Master, SFX, SC_Jump | Sound Classes and a sound used by the volume settings |
| Input | IA_ExampleMove, Look, Jump, Crouch, Sprint, ADS; IMC_Example | Remappable input actions and their mapping context |
