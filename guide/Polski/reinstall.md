<img align="right" src="https://github.com/n00b69/woa-dipper/blob/main/dipper.png" width="350" alt="Windows 11 running on dipper">

# Windows na Xiaomi Mi 8

## Ponowna instalacja Windows

### Wymagania
- [ADB i Fastboot](https://developer.android.com/studio/releases/platform-tools)

- [Zmodyfikowane recovery](https://github.com/n00b69/woa-dipper/releases/tag/Recovery)

### Uruchomienie zmodyfikowane recovery
> Jeśli recovery zostało zastąpione recovery domyślnym, sflashuj go ponownie za pomocą
```cmd
fastboot flash recovery ścieżka\do\modded-recovery-dipper.img reboot recovery
```

#### Formatowanie Windows
```cmd
adb shell format
```

## [Następny Krok: Ponowna instalacja Windows](3-install.md)






























