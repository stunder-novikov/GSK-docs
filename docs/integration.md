# Integration Guide

**The entire API is available from both C++ and Blueprint.** Use whichever is more convenient for your team.

## 1. Create Data Assets

Create Data Assets of type `GSK Settings Data`. Each Data Asset contains an array of settings (`FGSKSettingDefinition`).

Setting fields:

| Field | Description |
|-------|-------------|
| Setting Id | Unique identifier (FName), e.g. `"MasterVolume"` |
| Display Name | Name shown in UI |
| Description | Tooltip text |
| Category | Category from Project Settings (selected from dropdown) |
| Type | Bool, Int, Float, Enum, or Key |
| Console Variable | Engine cvar binding. Empty for custom logic. |
| Default Value | Default value as string |
| Min / Max Value | Range for Int/Float |
| Step Size | Slider step |
| Enum Options | Options for Enum type |
| Dynamic Enum Options | Populate options at runtime |
| Sort Order | Order within category |

## 2. Connect Data Assets

Project Settings -> Plugins -> Game Settings Kit -> Settings Data Assets -- add references to your Data Assets. For key bindings, do the same under Key Bindings Data Assets.

## 3. Build UI

Create a Widget Blueprint parented to `GSKSettingsWidget`:

1. Call `Initialize Settings` on Construct
2. Implement `On Settings Populated` event -- create row widgets
3. Implement `On Category Changed` event -- update tabs
4. Buttons: `On Apply Pressed`, `On Revert Pressed`, `On Defaults Pressed`

For setting rows, create widgets parented to `GSKSettingRowWidget`:

1. Call `Init Row(Definition)` when creating
2. Implement `On Row Initialized` -- set up the control (slider/checkbox/dropdown)
3. Implement `On Value Changed` -- update control when value changes

Or copy and modify the example widgets from `Example/Widgets/`.

## 4. Apply Game Settings

Subscribe to `OnSettingsApplied` to apply settings without built-in handlers (FOV, sensitivity, volume, etc.). See [Events](docs/api-events.md) for details.

## 5. Access the Manager

The manager is a GameInstance Subsystem, accessible from anywhere:

**Blueprint:**
```
Get GSKSettingsManager
```

**C++:**
```cpp
UGSKSettingsManager* Manager = GetGameInstance()->GetSubsystem<UGSKSettingsManager>();
```
