# API: Hardware Benchmark

## RunHardwareBenchmark

Runs UE hardware benchmark and sets optimal scalability settings.

**C++:**
```cpp
Manager->RunHardwareBenchmark();
```

**Blueprint:** `Run Hardware Benchmark`

Runs automatically on first launch if `bRunBenchmarkOnFirstLaunch = true` in Project Settings. Does not run in editor (PIE).
