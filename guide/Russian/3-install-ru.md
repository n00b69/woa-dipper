<img align="right" src="https://github.com/n00b69/woa-dipper/blob/main/dipper.png" width="350" alt="Windows 11 running on dipper">

# Запуск Windows на Xiaomi Mi 8

## Установка Windows

### Требования
- [Модифицированный OFOX recovery](https://github.com/n00b69/woa-dipper/releases/download/Files/modded-ofox-dipper.img)

- [Образ ARM Windows](https://arkt-7.github.io/woawin/)
  
- [Драйвера](https://github.com/n00b69/woa-dipper/releases/tag/Drivers)

- [Devcfg исправления touch](https://github.com/n00b69/woa-dipper/releases/download/Files/devcfg-dipper.img)

- [Образ UEFI](https://github.com/n00b69/woa-dipper/releases/tag/UEFI)

### Прошейте OFOX recovery
> Если ваше recovery было заменено стоковым, прошейте его снова используя
```cmd
fastboot flash recovery path\to\modded-ofox-dipper.img reboot recovery
```

#### Включите режим mass storage
> Если он попросит вас запустить его ещё раз, сделайте это
```cmd
adb shell msc
```

### Diskpart
> [!WARNING]
> НЕ УДАЛЯЙТЕ, НЕ СОЗДАВАЙТЕ И НЕ ИЗМЕНЯЙТЕ КАКИМ-ЛИБО ИНЫМ ОБРАЗОМ РАЗДЕЛЫ, НАХОДЯСЬ В DISKPART!!! ЭТО МОЖЕТ ПРИВЕСТИ К УДАЛЕНИЮ UFS ИЛИ НЕВОЗМОЖНОСТИ ЗАГРУЗКИ В FASTBOOT!!! ЭТО ОЗНАЧАЕТ, ЧТО ВАШЕ УСТРОЙСТВО БУДЕТ ОКИРПИЧЕНО БЕЗ КАКОГО-ЛИБО РЕШЕНИЯ! (за исключением доставки устройства в Xiaomi или его перепрошивки с помощью [EDL](edl-ru.md))
```cmd
diskpart
```

#### Выбрать раздел Windows 
> Используйте `list volume` чтобы найти его, замените `$` номером раздела **WINDIPPER**
```cmd
select volume $
``` 

#### Добавить букву к разделу Windows
```cmd
assign letter x
``` 

#### Выбрать раздел ESP
> Используйте `list volume` чтобы найти его, замените `$` номером раздела **ESPDIPPER**
```cmd
select volume $
``` 

#### Добавьте букву к ESP
```cmd
assign letter y
```

#### Выйти из diskpart
```cmd
exit
```

### Установка Windows
> [!Warning]
> НЕ ИСПОЛЬЗУЙТЕ 24H2!!!

> Замените `путь\к\install.esd` актуальным путём к install.esd (файл также может называться install.wim или 22631.2861.XXXXXXX.esd)
```cmd
dism /apply-image /ImageFile:путь\к\install.esd /index:6 /ApplyDir:X:\
```

> Если вы получите `Error 87`, проверьте индекс вышего образа используя `dism /get-imageinfo /ImageFile:путь\к\install.esd`, затем замените `index:6` действтельным индексом Windows 11 Pro в вашем образе

### Копирование вашего boot.img в Windows
- Перетащите **rooted_boot.img** на диск **WINDIPPER** в проводнике Windows, затем переименуйте его в **boot.img**.

### Установка драйверов
- Распакуйте пакет драйверов, затем откройте файл `OfflineUpdater.cmd` (Если появляется ошибка, запустите `OfflineUpdaterFix.cmd`)

> Введите букву диска **WINDIPPER** (должна быть **X**) затем нажмите Enter
  
#### Создать файлы загрузчика Windows
> Если возникнет какая-либо ошибка, например "Сбой при инициализации системного тома библиотеки", снова откройте `diskpart` и назначьте **ESPDIPPER** любую новую букву, затем замените букву `Y` в следующих командах на букву, которую вы только что добавили.
```cmd
bcdboot X:\Windows /s Y: /f UEFI
```

#### Включение тестовой подпись
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" testsigning on
```

#### Отключите восстановление
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" recoveryenabled no
```

#### Отключите проверку целостности
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" nointegritychecks on
```

#### Удалите букву диска для ESP
> Если это не сработает, проигнорируйте это и перейдите к следующей команде. Этот фантомный диск исчезнет при следующей перезагрузке ПК.
```cmd
mountvol y: /d
```

### Перезагрузитесь в fastboot
```cmd
adb reboot bootloader
```

### Исправить touch
> Перезагрузитесь в fastboot, затем замените `путь\к\devcfg-dipper.img` путём к образу
```cmd
fastboot flash devcfg_ab путь\к\devcfg-dipper.img
```

#### Загрузитесь в UEFI
> Замените `путь\к\dipper-uefi.img` актуальным путём к образу UEFI

> [!Important]
> Remove your USB cable right after leaving the fastboot screen, or Windows may crash in the initial setup
```cmd
fastboot boot путь\к\dipper-uefi.img
```

### Reboot to Android
Your device should reboot by itself after +- 10 minutes of waiting, after which you will be booted into Android, for the last step.

## [Последний шаг: Настройка двойной загрузки](4-dualboot-ru.md)
