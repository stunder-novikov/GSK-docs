# API: Dynamic Enum Options

## Built-in Providers

Set `Dynamic Enum Options = true` in Data Asset:

| Setting Id | What Gets Populated |
|-----------|---------------------|
| Resolution | Supported screen resolutions |
| UpscaleMethod | None, FXAA, TAA, TSR + DLSS/FSR if available |
| AudioOutputDevice | System audio output devices |

## Custom Provider

**C++:**
```cpp
FGSKDynamicOptionsDelegate Delegate;
Delegate.BindDynamic(this, &UMyClass::GetLanguageOptions);
Manager->RegisterDynamicOptionsProvider(FName("Language"), Delegate);

// Provider function:
TArray<FText> UMyClass::GetLanguageOptions(FName SettingId)
{
    return { FText::FromString("English"), FText::FromString("Russian"), FText::FromString("Japanese") };
}
```

**Blueprint:** `Register Dynamic Options Provider (SettingId, Provider)` -- Provider is a delegate. Create a Custom Event with return type `Array of Text` and parameter `SettingId (Name)`.
