# API: Dynamic Enum Options

## Built-in Providers

Set `Dynamic Enum Options = true` in Data Asset:

| Setting Id | What Gets Populated |
|-----------|---------------------|
| Resolution | Supported screen resolutions. Default: the desktop resolution. Saved as text (e.g. `1920x1080`); if the saved resolution is missing on another display, the largest one that fits is used. |
| UpscaleMethod | None, FXAA, TAA, TSR, plus DLSS/FSR when their plugins are enabled. Saved by name. |
| AudioOutputDevice | System audio output devices (filled shortly after start; fires OnSettingOptionsUpdated) |

## Custom Provider

**C++:**
```cpp
FGSKDynamicOptionsDelegate Delegate;
Delegate.BindDynamic(this, &UMyClass::GetLanguageOptions);
Manager->RegisterDynamicOptionsProvider(FName("Language"), Delegate);

// The provider must be a UFUNCTION()
// Provider function:
TArray<FText> UMyClass::GetLanguageOptions(FName SettingId)
{
    return { FText::FromString("English"), FText::FromString("Russian"), FText::FromString("Japanese") };
}
```

**Blueprint:** `Register Dynamic Options Provider (SettingId, Provider)` -- Provider is a delegate. Create a Custom Event with return type `Array of Text` and parameter `SettingId (Name)`.

A provider registered after the game starts (e.g. in BeginPlay) is not copied into the setting's definition. Read the options with `Get Enum Options For Setting` in your row widget. The example `WBP_SettingRow_Enum` reads `Definition.EnumOptions` and must be changed for this. Custom dynamic settings are saved as option indices.
