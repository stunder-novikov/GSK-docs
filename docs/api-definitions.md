# API: Settings Definitions

## GetSettingsForCategory

Returns all settings for a given category.

**C++:**
```cpp
TArray<FGSKSettingDefinition> DisplaySettings = Manager->GetSettingsForCategory(FName("Display"));
```

**Blueprint:** `Get Settings For Category (InCategory: "Display")`

## GetSettingDefinition

Get a specific setting definition by ID.

**C++:**
```cpp
FGSKSettingDefinition Def;
if (Manager->GetSettingDefinition(FName("MasterVolume"), Def))
{
    UE_LOG(LogTemp, Log, TEXT("Min: %f, Max: %f"), Def.MinValue, Def.MaxValue);
}
```

**Blueprint:** `Get Setting Definition (SettingId, OutDefinition) -> bool`

## GetEnumOptionsForSetting

Get options for an Enum setting (static from Data Asset or dynamic).

**C++:**
```cpp
TArray<FText> Options = Manager->GetEnumOptionsForSetting(FName("Resolution"));
```

**Blueprint:** `Get Enum Options For Setting (SettingId) -> Array of Text`
