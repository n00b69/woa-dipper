<img align="right" src="https://github.com/n00b69/woa-dipper/blob/main/dipper.png" width="350" alt="Windows 11 running on dipper">

# Запуск Windows на Xiaomi Mi 8

## Обновление драйверов 

### Требования
- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)

- [Модифицированный OFOX recovery](https://github.com/n00b69/woa-dipper/releases/download/Files/modded-ofox-dipper.img)
  
- [Драйвера](https://github.com/n00b69/woa-dipper/releases/tag/Drivers)
  
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
```cmd
diskpart
```

#### Выбрать раздел Windows 
> Используйте `list volume` чтобы найти его, замените `$` номером раздела **WINDIPPER**
```diskpart
select volume $
```

#### Добавить букву к разделу Windows
```cmd
assign letter X
```

### Выйти из diskpart
```cmd
exit
```

### Установка драйверов 
> [!Note]
> Этот процесс займёт +- 20 минут. Не волнуйтесь, это нормально.

- Распакуйте пакет драйверов, затем откройте файл `OfflineUpdater.cmd` (Если появляется ошибка, запустите `OfflineUpdaterFix.cmd`)

> Введите букву диска **WINDIPPER** (должна быть **X**) затем нажмите Enter

### Reboot your device
> Не забудьте также заменить образ UEFI в Android, иначе вы можете столкнуться с "синим экраном смерти" (BSoD) при последующей загрузке в Windows.
```cmd
adb reboot
```

## Готово!




































