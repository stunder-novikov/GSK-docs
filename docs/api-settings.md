# API: Read & Write Settings

## GetSettingValue / SetSettingValue

Get/set a setting value as string.

**C++:**
```cpp
FString Value = Manager->GetSettingValue(FName("MasterVolume"));
Manager->SetSettingValue(FName("MasterVolume"), TEXT("75"));
```

**Blueprint:**
```
Get Setting Value (SettingId: "MasterVolume") -> String
Set Setting Value (SettingId: "MasterVolume", Value: "75")
```

## Typed Getters/Setters

| Method | C++ | Blueprint |
|--------|-----|-----------|
| `GetSettingFloat(Id)` | `float Vol = Manager->GetSettingFloat(FName("MasterVolume"));` | Get Setting Float |
| `GetSettingInt(Id)` | `int32 Qual = Manager->GetSettingInt(FName("TextureQuality"));` | Get Setting Int |
| `GetSettingBool(Id)` | `bool bVSync = Manager->GetSettingBool(FName("VSync"));` | Get Setting Bool |
| `SetSettingFloat(Id, Value)` | `Manager->SetSettingFloat(FName("MasterVolume"), 0.8f);` | Set Setting Float |
| `SetSettingInt(Id, Value)` | `Manager->SetSettingInt(FName("TextureQuality"), 2);` | Set Setting Int |
| `SetSettingBool(Id, Value)` | `Manager->SetSettingBool(FName("VSync"), true);` | Set Setting Bool |

> All Set methods modify the **pending** value. It is not applied until `ApplySettings()` is called.
