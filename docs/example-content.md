# Example Content

The plugin includes a working example in `Content/GameSettingsKit/Example/`:

## Data Assets

| Asset | Description |
|-------|-------------|
| DA_DisplaySettings | Resolution, display mode, VSync, FPS limit, brightness, FOV |
| DA_GraphicsSettings | Overall Quality, 10 individual settings, post-process toggles, upscaler |
| DA_AudioSettings | 5 volume sliders + output device |
| DA_InputSettings | Mouse sensitivity, ADS sensitivity, invert Y |
| DA_GameplaySettings | HUD scale, FPS counter, crouch/sprint/ADS modes |
| DA_KeyBindings | References to example IMC |

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
