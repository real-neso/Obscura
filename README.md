# Obscura Open Client

This directory contains the open-source client for Obscura.

## Architecture

The project is divided into two parts:
1. **obscura-open**: This repository. Contains UI, ViewModels, and Network logic.
2. **obscura-private**: (Private) Contains sensitive cryptographic implementations and native security code.

## ObscuraEngine

All sensitive operations are abstracted behind the `ObscuraEngine` interface.
Developers can implement this interface to provide their own security logic or use the official private core.

```kotlin
interface ObscuraEngine {
    fun isDeviceCompromised(context: Context): Boolean
    fun getSecurityAuditCode(context: Context): Long
    // ...
}
```

## Integration

To initialize the `NetworkClient`, you must provide an implementation of `ObscuraEngine`:

```kotlin
NetworkClient.init(context, myEngineImplementation)
```

## Security Note

Sensitive values such as salts and signature hashes should be managed via `secrets.properties`. A template is provided in `secrets.properties.example`.
