# API: Key Remapping

## Prerequisites

1. Project Settings -> Enhanced Input -> **Enable User Settings** = true
2. On Input Actions, enable **Is Player Mappable** and set a Display Name
3. Create a Data Asset of type `GSK Key Bindings Data` with references to your IMCs
4. Add it to Project Settings -> Game Settings Kit -> Key Bindings Data Assets

## GetAllKeyBindings

Get all remappable bindings.

**C++:**
```cpp
TArray<FGSKKeyBindingInfo> Bindings = Manager->GetAllKeyBindings();
for (const FGSKKeyBindingInfo& Info : Bindings)
{
    UE_LOG(LogTemp, Log, TEXT("%s: %s (default: %s)"),
        *Info.DisplayName.ToString(),
        *Info.CurrentKey.ToString(),
        *Info.DefaultKey.ToString());
}
```

**Blueprint:** `Get All Key Bindings -> Array of GSKKeyBindingInfo`

Each element contains:
- `DisplayName` -- action display name
- `MappingName` -- internal name for remapping
- `CurrentKey` -- currently bound key
- `DefaultKey` -- default key
- `bIsPrimarySlot` -- primary slot
- `bIsCustomized` -- changed by user

## RemapKey

**C++:**
```cpp
FText FailReason;
bool bSuccess = Manager->RemapKey(FName("IA_Jump"), FKey("F"), true, FailReason);
if (!bSuccess)
{
    UE_LOG(LogTemp, Warning, TEXT("Remap failed: %s"), *FailReason.ToString());
}
```

**Blueprint:** `Remap Key (MappingName, NewKey, bIsPrimarySlot, OutFailureReason) -> bool`

## ResetKeyToDefault / ResetAllKeysToDefaults

**C++:**
```cpp
Manager->ResetKeyToDefault(FName("IA_Jump"), true);   // Single
Manager->ResetAllKeysToDefaults();                      // All
```

**Blueprint:** `Reset Key To Default (MappingName, bIsPrimarySlot)`, `Reset All Keys To Defaults`

## SaveKeyBindings

**C++:**
```cpp
Manager->SaveKeyBindings();
```

**Blueprint:** `Save Key Bindings`

## IsKeyRemappingAvailable

**C++:**
```cpp
if (Manager->IsKeyRemappingAvailable())
{
    // Show remapping UI
}
```

**Blueprint:** `Is Key Remapping Available -> bool`

> Returns false if Enhanced Input User Settings are not enabled.

## Mouse Button Capture

The standard `InputKeySelector` widget does not capture mouse buttons. Use a full-screen transparent overlay widget that handles `OnKeyDown` and `OnMouseButtonDown` events. See `WBP_CaptureOverlay` in example content.
