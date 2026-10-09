# API: Hardware Benchmark

## RunHardwareBenchmark

Runs UE hardware benchmark and sets optimal scalability settings.

**C++:**
```cpp
Manager->RunHardwareBenchmark();
```

**Blueprint:** `Run Hardware Benchmark`

Runs automatically on first launch if **Run Benchmark On First Launch** is enabled in Project Settings (default: on). First launch means no Game Settings Kit values have been saved yet. Saves made by version 1.0.0 count as already launched. It does not run in the editor (PIE), only in packaged and standalone games, and its result is applied and saved immediately.

When you call it yourself, the engine applies the detected quality levels at once and the manager's quality settings become pending. Call `Apply Settings` to keep them.
