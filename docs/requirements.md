# Requirements

- Unreal Engine 5.7 or 5.8
- Enhanced Input plugin (enabled by default). Key remapping also needs the Enhanced Input default input classes and **Enable User Settings** (on by default in 5.8, off in 5.7) -- see [Quick Start](docs/quickstart.md).
- For DLSS: NVIDIA's DLSS plugin. For FSR: AMD's FSR plugin (FFXFSRTemporalUpscaling). Neither is included.
  Game Settings Kit lists DLSS/FSR when the vendor plugin is enabled in the project; it does not check whether the player's GPU supports it.

## Known limitations

- The settings manager is not created on a dedicated server. Code shared with a server must check `GetSubsystem<UGSKSettingsManager>()` (Blueprint: Is Valid) for null.
- Aggregate audio devices (an engine option, off by default) report a different device id after a switch, so every Apply switches the output device again.
- With several Play In Editor clients, audio device events of one client can disturb another client's record of the device in use. Packaged games are unaffected.
- UE 5.7 can accept an output-device switch and never perform it; the same device is then not requested again until the next device change.
- Console variables your project sets above scalability priority (`[SystemSettings]`, ConsoleVariables.ini, device profiles, command line, console) win over the player's post-process and resolution-scale settings. See [Built-in Handlers](docs/handlers.md).

## Support

Discord: https://discord.gg/yc7xswkq3R

Fab: https://www.fab.com/listings/9d2305f7-1e80-476a-b299-123190a1ee73
