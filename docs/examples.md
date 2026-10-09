# Examples: Custom Settings

## Example 1: Add Language Setting

1. In Project Settings -> Plugins -> Game Settings Kit -> Categories, add `"Localization"` (or use existing Gameplay)
2. In Data Asset, create a setting:
   - Setting Id: `Language`
   - Type: Enum
   - Dynamic Enum Options: true
3. Register a provider (GetLanguages must be declared as a UFUNCTION() in the header):

```cpp
void AMyGameMode::BeginPlay()
{
    auto* Manager = GetGameInstance()->GetSubsystem<UGSKSettingsManager>();
    FGSKDynamicOptionsDelegate Delegate;
    Delegate.BindDynamic(this, &AMyGameMode::GetLanguages);
    Manager->RegisterDynamicOptionsProvider(FName("Language"), Delegate);
}

TArray<FText> AMyGameMode::GetLanguages(FName SettingId)
{
    return { FText::FromString("English"), FText::FromString("Russian") };
}
```

Because this provider is registered in BeginPlay, your Enum row must read its options with `Get Enum Options For Setting` -- see [Dynamic Enum Options](docs/api-dynamic.md).

4. In `OnSettingsApplied`, apply:

```cpp
int32 LangIndex = Manager->GetSettingInt(FName("Language"));
// Apply localization
```

## Example 2: Accessibility - Subtitle Size

1. In Project Settings -> Plugins -> Game Settings Kit -> Categories, add `"Accessibility"`
2. In Data Asset:
   - Setting Id: `SubtitleSize`
   - Category: Accessibility
   - Type: Float
   - Min: 12, Max: 36, Step: 2
   - Default: 18
3. In `OnSettingsApplied`:

```cpp
float Size = Manager->GetSettingFloat(FName("SubtitleSize"));
SubtitleWidget->SetFontSize(Size);
```
