# API: Apply / Revert / Defaults

## ApplySettings

Applies all pending values to the engine and saves to disk. Every setting is applied, not only the changed ones.

**C++:**
```cpp
Manager->ApplySettings();
```

**Blueprint:** `Apply Settings`

## RevertSettings

Discards pending changes, restores last applied values.

**C++:**
```cpp
Manager->RevertSettings();
```

**Blueprint:** `Revert Settings`

## ResetToDefaults

Resets all settings to default values from Data Assets. Values become pending -- call `ApplySettings()` to apply. Not to be confused with **Reset Data Assets to Defaults** in Project Settings, which resets the Data Asset lists.

**C++:**
```cpp
Manager->ResetToDefaults();
Manager->ApplySettings(); // Apply defaults
```

**Blueprint:** `Reset To Defaults`, then `Apply Settings`

## HasPendingChanges

Returns true when any pending value differs from the last applied one.

**C++:**
```cpp
if (Manager->HasPendingChanges())
{
    // Show "unsaved changes" dialog
}
```

**Blueprint:** `Has Pending Changes -> bool`

## Where values are saved

Player values are saved in `GameUserSettings.ini`, section `[GameSettingsKit.Settings]`:
- Packaged Windows game: `%LOCALAPPDATA%\<ProjectName>\Saved\Config\Windows\GameUserSettings.ini`
- Editor / PIE: `<Project>\Saved\Config\WindowsEditor\GameUserSettings.ini`

Enum settings are saved as option indices, except Resolution (e.g. `1920x1080`) and UpscaleMethod (e.g. `TSR`) when the plugin fills their options. The audio device is also saved as `AudioOutputDevice.DeviceId`. The key `GSKInitialized=True` records that settings have been saved; delete the section to simulate a first launch.

Key bindings are saved by Enhanced Input in a SaveGame slot (Project Settings -> Enhanced Input -> Input Settings Save Slot Name, default `EnhancedInputUserSettings`) under `Saved/SaveGames`.
