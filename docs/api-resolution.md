# API: Resolution Confirmation

## Workflow

```
1. User changes resolution / display mode
2. ApplySettings()
3. if (Manager->DidResolutionChange())
4.     Show GSKResolutionConfirmWidget
5.     Widget->StartConfirmation(15.0f)
6. User confirms -> ConfirmResolution()
   or timer expires -> RevertResolution() (automatic)
```

## DidResolutionChange

**C++:**
```cpp
Manager->ApplySettings();
if (Manager->DidResolutionChange())
{
    // Show confirmation dialog
}
```

**Blueprint:** `Did Resolution Change -> bool`

## StartResolutionConfirmation

**C++:**
```cpp
Manager->StartResolutionConfirmation(15.0f);
```

**Blueprint:** `Start Resolution Confirmation (TimeoutSeconds: 15.0)`

## ConfirmResolution / RevertResolution

**C++:**
```cpp
Manager->ConfirmResolution();  // Keep new resolution
Manager->RevertResolution();   // Revert to old resolution
```

**Blueprint:** `Confirm Resolution`, `Revert Resolution`

## GSKResolutionConfirmWidget

Blueprint events:
- `On Countdown Tick(RemainingSeconds)` -- update countdown text
- `On Timer Expired` -- timer expired, resolution reverted

Methods:
- `Start Confirmation(TimeoutSeconds)` -- start timer
- `On Confirm Pressed` -- user confirmed
- `On Revert Pressed` -- user canceled
- `Get Remaining Seconds` -- remaining time
