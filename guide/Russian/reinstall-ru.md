<img align="right" src="https://github.com/n00b69/woa-polaris/blob/main/polaris.png" width="350" alt="Windows 11 running on dipper">

# Запуск Windows на Xiaomi Mi 8

## Переустановка Windows

### Требования
- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)

- [Модифицированный recovery](https://github.com/n00b69/woa-dipper/releases/tag/Recovery)

### Прошейте Модифицированный recovery
> Если ваше recovery было заменено стоковым, прошейте его снова используя
```cmd
fastboot flash recovery path\to\modded-recovery-dipper.img reboot recovery
```

#### Отформатировать раздел Windows
```cmd
adb shell format
```

## [Следующий шаг: Установка Windows](3-install-ru.md)


























