# Quick Start

> Upgrading from 1.0.0? Delete the old plugin folder before installing 1.1.0 -- see [Changelog](docs/changelog.md).

## 1. Enable Plugin

Edit -> Plugins -> Game Settings Kit -> Enable. Restart the editor.

## 2. Set Up Enhanced Input for Key Remapping

Key remapping needs two Enhanced Input settings:

1. Project Settings -> Engine -> Input -> Default Classes: **Default Player Input Class** = `EnhancedPlayerInput` and **Default Input Component Class** = `EnhancedInputComponent`. Projects created from UE5 templates already have these; check them in projects converted from UE4 or created without a template.
2. Project Settings -> Engine -> Enhanced Input -> **Enable User Settings** = true. On by default in UE 5.8, off by default in UE 5.7.

If either is missing, remapping is unavailable (no key bindings are listed) and the log shows:

- `UEnhancedInputLocalPlayerSubsystem for Local Player '...' does not have a valid PlayerInput object. Failed to load user settings.` -- the default input classes are not the Enhanced Input ones.
- `Enhanced Input User Settings not available. Enable 'User Settings' in Project Settings > Enhanced Input.` -- logged by Game Settings Kit when either setting is missing.

## 3. Open Example

Open the map `/GameSettingsKit/Example/Maps/L_SettingsExample` (Content Browser: enable **Settings > Show Plugin Content**, then **Plugins > Game Settings Kit Content > Example > Maps**). Press Play, press Escape -- you'll see a fully working settings menu with all categories: Display, Graphics, Audio, Input, Gameplay.

Explore the example: Data Assets in `/GameSettingsKit/Example/Data/`, widgets in `/GameSettingsKit/Example/Widgets/`, Blueprints in `/GameSettingsKit/Example/Blueprints/`. Use as reference for integrating into your own project.
