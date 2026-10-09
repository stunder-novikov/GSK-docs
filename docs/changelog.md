# Changelog

## 1.1.0

### Upgrading from 1.0.0

1. Close the editor and **delete the old `GameSettingsKit` plugin folder** before installing 1.1.0. Version 1.0.0 shipped `Config/DefaultGameSettingsKit.ini` inside the plugin; 1.1.0 no longer does, and a leftover copy would keep re-adding the example Data Assets.
2. Open the project in the editor once. Your Data Asset lists are kept; if you never configured any, the examples are listed. The editor saves this in your project's `Config/DefaultGameSettingsKit.ini` -- commit that file.
3. Players' saved settings carry over. Resolution and upscaler saves from 1.0.0 are read once and re-saved in the new format; the hardware benchmark does not run again.

### Fixes

- Players' saved settings are no longer overwritten by defaults in projects whose Data Assets have no Brightness setting.
- **Run Benchmark On First Launch** is now respected.
- Unconfirmed resolution changes now revert while the game is paused, are not kept when the game quits, and revert to the last confirmed values after several unconfirmed changes.
- The audio output device is switched only when the player picks another one; a choice made right after an Apply is no longer refused, and the choice is restored after the engine switches devices by itself. The menu no longer shows unapplied changes right after start.
- Play In Editor no longer leaves the editor with the game's graphics settings, frame rate cap or Sound Class volumes, during the session or after an editor restart.
- Saved enum values that match no option are replaced by the default (Overall Quality: Custom).
- Example Data Assets are packaged even when the project's config file was not written before cooking.
- Packaged games, dedicated servers and commandlets no longer write the project's config file.
- A setting row initialized twice is bound once (no ensure in development builds).
- No console-manager warnings for resolution scale and post-process settings; no "empty engine version" warnings; the example map passes map check with nothing to build.

### Changes

- Post-process effects switched on now follow the quality level instead of forcing maximum. Off is still off.
- Values your project sets for these console variables (`[SystemSettings]`, ConsoleVariables.ini, device profiles, command line, console) now win over the player's setting.
- `-ResX`, `-ResY`, `-Windowed`, `-FullScreen` win over the saved display settings at startup.
- Resolution is saved as `WxH` and the upscaler by name, with fallbacks when they are unavailable.
- New: `IsResolutionConfirmationPending`, `GetResolutionConfirmationSecondsLeft`. The confirmation dialog shows the manager's countdown and closes when the confirmation ends.
- The settings manager is not created on dedicated servers.
- Example Data Assets are set up from code on first editor start; new Project Settings button **Reset Data Assets to Defaults**.

### Compatibility

- Unreal Engine 5.7 and 5.8.
- Key remapping needs the Enhanced Input default input classes and **Enable User Settings** (on by default in 5.8, off in 5.7) -- see [Quick Start](docs/quickstart.md).

## 1.0.0

- Initial release for Unreal Engine 5.7.
