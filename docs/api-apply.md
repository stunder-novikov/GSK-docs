# API: Apply / Revert / Defaults

## ApplySettings

Applies all pending values to the engine and saves to disk.

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

Resets all settings to default values from Data Assets. Values become pending -- call `ApplySettings()` to apply.

**C++:**
```cpp
Manager->ResetToDefaults();
Manager->ApplySettings(); // Apply defaults
```

**Blueprint:** `Reset To Defaults`, then `Apply Settings`

## HasPendingChanges

Checks if there are unsaved changes.

**C++:**
```cpp
if (Manager->HasPendingChanges())
{
    // Show "unsaved changes" dialog
}
```

**Blueprint:** `Has Pending Changes -> bool`
