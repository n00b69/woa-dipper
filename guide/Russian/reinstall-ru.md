<img align="right" src="https://github.com/n00b69/woa-polaris/blob/main/polaris.png" width="350" alt="Windows 11 running on dipper">

# Запуск Windows на Xiaomi Mi 8

## Переустановка Windows

### Требования
- [Образ ARM Windows](https://worproject.com/esd)
  
- [Драйвера](https://github.com/n00b69/woa-dipper/releases/tag/Drivers)
  
- [Образ UEFI](https://github.com/n00b69/woa-dipper/releases/tag/UEFI)

### Загрузитесь в UEFI
> Замените `путь\к\dipper-uefi.img` действительным путём к образу UEFI
```cmd
fastboot boot путь\к\dipper-uefi.img
```

#### Включите режим mass storage
> После загрузки в UEFI используйте кнопки регулировки громкости для навигации по меню и кнопку питания для подтверждения
- Выберите **UEFI Boot Menu**.
- Выберите **USB Attached SCSI (UAS) Storage**.
- Нажмите кнопку **питания** дважды чтобы подтвердить.

### Diskpart
```cmd
diskpart
```

#### Найдите диск вашего телефона
> При этом отобразится список всех подключенных дисков
```cmd
lis dis
```

#### Выберите диск вашего телефона
> Замените `$` актуальным номером диска вашего телефона (должен быть последним)
```cmd
sel dis $
```

#### Отобразите список разделов вашего телефона
> Это отобразит список разделов вашего телефона 
```cmd
lis par
```

#### Выберите раздел Windows 
> Замените `$` номером раздела Windows (должен быть 23)
```cmd
sel par $
```

#### Добавьте букву к разделу Windows
```cmd
assign letter X
```

#### Выйдите из diskpart
```cmd
exit
```

#### Отформатируйте раздел Windows
> Перейдите в Проводник Windows > Этот компьютер и выберите **WINDIPPER**. Щелкните правой кнопкой мыши и отформатируйте как NTFS.

### Установка Windows
> Замените `путь\к\install.esd` актуальным путём к install.esd (файл также может называться install.wim)
```cmd
dism /apply-image /ImageFile:путь\к\install.esd /index:6 /ApplyDir:X:\
```

> Если вы получите `Error 87`, проверьте индекс вышего образа используя `dism /get-imageinfo /ImageFile:<путь\к\install.esd>`, затем замените `index:6` действтельным индексом Windows 11 Pro в вашем образе

### Установка драйверов
> Распакуйте пакет драйверов, затем откройте файл `OfflineUpdater.cmd` (if an error shows up, run `OfflineUpdaterFix.cmd` instead)

> Введите букву диска **WINDIPPER** (должна быть **X**) затем нажмите Enter

### Загрузка в Windows
Перезагрузите телефон. Если в итоге он загрузится в Android, а не в Windows, перепрошейте UEFI заново с помощью WOA Helper.

#### Настройка Windows
> Сейчас Windows на вашем устройстве настроится. Это займёт некоторое время. В конечном итоге телефон перезагрузится, и после этого должна запуститься программа начальной установки (oobe).

> [!Tip]
> If you wish to skip the Microsoft Account login, press the **I don't have internet** button in the WiFi page, then when prompted, press the **Continue with limited setup** button.

## Готово!











