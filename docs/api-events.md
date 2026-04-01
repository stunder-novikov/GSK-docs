# API: Events

## OnSettingChanged

Fires when any pending value changes.

**C++:**
```cpp
Manager->OnSettingChanged.AddDynamic(this, &UMyClass::HandleSettingChanged);

void UMyClass::HandleSettingChanged(FName SettingId, const FString& NewValue)
{
    if (SettingId == FName("FOV"))
    {
        float FOV = FCString::Atof(*NewValue);
        // Update camera preview
    }
}
```

**Blueprint:** `Bind Event to On Setting Changed`

## OnSettingsApplied

Fires after `ApplySettings()`. Use to apply game-specific settings (FOV, sensitivity, volume, etc.).

**C++:**
```cpp
Manager->OnSettingsApplied.AddDynamic(this, &AMyGameMode::OnSettingsApplied);

void AMyGameMode::OnSettingsApplied()
{
    UGSKSettingsManager* Mgr = GetGameInstance()->GetSubsystem<UGSKSettingsManager>();
    float Sens = Mgr->GetSettingFloat(FName("MouseSensitivity"));
    float FOV = Mgr->GetSettingFloat(FName("FOV"));
    // Apply to character
}
```

**Blueprint:** `Bind Event to On Settings Applied`

## OnSettingsReverted

Fires after `RevertSettings()`.

**Blueprint:** `Bind Event to On Settings Reverted`

## OnAudioDevicesReady

Fires when audio device list is loaded.

**Blueprint:** `Bind Event to On Audio Devices Ready`

## OnSettingOptionsUpdated

Fires when dynamic enum options changed for a setting (e.g. after audio device discovery).

**C++:**
```cpp
Manager->OnSettingOptionsUpdated.AddDynamic(this, &UMyWidget::HandleOptionsUpdated);

void UMyWidget::HandleOptionsUpdated(FName SettingId)
{
    if (SettingId == FName("AudioOutputDevice"))
    {
        // Rebuild dropdown
    }
}
```

**Blueprint:** `Bind Event to On Setting Options Updated`

## OnKeyBindingsRefreshed

Fires when key bindings list is updated.

**Blueprint:** `Bind Event to On Key Bindings Refreshed`
