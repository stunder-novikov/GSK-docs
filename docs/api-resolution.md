# API: Resolution Confirmation

## Workflow

```
1. User changes resolution / display mode
2. ApplySettings()
3. if (Manager->DidResolutionChange())
4.     Show GSKResolutionConfirmWidget
5.     Widget->StartConfirmation(15.0f)
6. User confirms -> ConfirmResolution()
   or the countdown ends -> RevertResolution() (automatic, also while the game is paused)
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

True when the last Apply changed Resolution or DisplayMode.

## StartResolutionConfirmation

**C++:**
```cpp
Manager->StartResolutionConfirmation(15.0f);
```

**Blueprint:** `Start Resolution Confirmation (TimeoutSeconds: 15.0)`

The countdown runs in real time, also while the game is paused. A timeout of 0 or less reverts on the next frame.

If the player applies another resolution change before confirming, a revert still goes back to the last *confirmed* values. A revert restores all settings to those values, including non-display settings applied in between. If the game quits while a change is unconfirmed, the change is not kept: the next start uses the last confirmed values.

## IsResolutionConfirmationPending / GetResolutionConfirmationSecondsLeft

**C++:**
```cpp
if (Manager->IsResolutionConfirmationPending())
{
    float Left = Manager->GetResolutionConfirmationSecondsLeft(); // 0 when none is pending
}
```

**Blueprint:** `Is Resolution Confirmation Pending -> bool`, `Get Resolution Confirmation Seconds Left -> float`

## ConfirmResolution / RevertResolution

**C++:**
```cpp
Manager->ConfirmResolution();  // Keep new resolution
Manager->RevertResolution();   // Revert to old resolution
```

**Blueprint:** `Confirm Resolution`, `Revert Resolution`

RevertResolution also fires OnSettingsReverted.

## GSKResolutionConfirmWidget

Blueprint events:
- `On Countdown Tick(RemainingSeconds)` -- update countdown text (the manager keeps the countdown)
- `On Timer Expired` -- the dialog is closing without Confirm: the countdown ended, Revert was pressed, or the confirmation was ended elsewhere

Methods:
- `Start Confirmation(TimeoutSeconds)` -- start the countdown
- `On Confirm Pressed` -- user confirmed; closes the dialog
- `On Revert Pressed` -- user reverted; closes the dialog
- `Get Remaining Seconds` -- remaining time

The dialog removes itself when the confirmation ends.
