<img align="right" src="https://github.com/n00b69/woa-dipper/blob/main/dipper.png" width="350" alt="Windows 11 running on dipper">

# Running Windows on the Xiaomi Mi 8

## Reinstalling Windows

### Prerequisites
- [Modded OFOX recovery](https://github.com/n00b69/woa-dipper/releases/download/Files/modded-ofox-dipper.img)

### Boot into OFOX
> If MIUI has replaced your recovery, boot to fastboot and run
```cmd
fastboot flash recovery path\to\modded-ofox-dipper.img reboot recovery
```

#### Formatting the Windows partition
```cmd
adb shell format
```

## [Next step: Reinstalling Windows](3-install.md)


















