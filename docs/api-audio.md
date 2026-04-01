# API: Audio

## SetSoundClassVolume (static)

Set volume on a Sound Class directly without Sound Mix.

**C++:**
```cpp
USoundClass* MasterClass = LoadObject<USoundClass>(nullptr, TEXT("/Game/Audio/Master.Master"));
UGSKSettingsManager::SetSoundClassVolume(MasterClass, 0.8f);
```

**Blueprint:** `Set Sound Class Volume (SoundClass, Volume 0-1)`

**Example with settings:**
```cpp
void AMyGameMode::OnSettingsApplied()
{
    UGSKSettingsManager* Manager = GetGameInstance()->GetSubsystem<UGSKSettingsManager>();
    float MasterVol = Manager->GetSettingFloat(FName("MasterVolume")) * 0.01f; // 0-100 -> 0-1
    UGSKSettingsManager::SetSoundClassVolume(MasterSoundClass, MasterVol);
}
```

## RequestAudioOutputDevices

Request list of audio output devices (async).

**C++:**
```cpp
Manager->RequestAudioOutputDevices();
// Subscribe to OnAudioDevicesReady for results
```

**Blueprint:** `Request Audio Output Devices`

Call when opening the Audio tab to detect connected/disconnected devices (hot-plug).

## SetAudioOutputDevice

Switch audio output device by DeviceId.

**C++:**
```cpp
Manager->SetAudioOutputDevice(DeviceId);
```

**Blueprint:** `Set Audio Output Device (DeviceId)`

> Usually not called directly -- the built-in AudioOutputDevice handler does this automatically on Apply.

## GetCachedAudioOutputDeviceNames / GetCachedAudioOutputDeviceIds

Get cached lists of device names and IDs after `RequestAudioOutputDevices`.

**C++:**
```cpp
const TArray<FString>& Names = Manager->GetCachedAudioOutputDeviceNames();
const TArray<FString>& Ids = Manager->GetCachedAudioOutputDeviceIds();
```

**Blueprint:** `Get Cached Audio Output Device Names -> Array of String`, `Get Cached Audio Output Device Ids -> Array of String`
