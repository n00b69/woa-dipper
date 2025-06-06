<img align="right" src="https://github.com/n00b69/woa-dipper/blob/main/dipper.png" width="350" alt="Windows 11 running on dipper">

# Запуск Windows на Xiaomi Mi 8

## Разметка устройства 

### Требования 
- Разблокированный Загрузчик

- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)
  
- [Модифицированный recovery](https://github.com/n00b69/woa-dipper/releases/tag/Recovery)

### Заметки 
> [!WARNING]  
> 
> НЕ ПЕРЕЗАГРУЖАЙТЕ ТЕЛЕФОН! Если вы считаете, что допустили ошибку, обратитесь за помощью в [Telegram чате](https://t.me/woadipper).
> 
> Не выполняйте все команды сразу, выполняйте их по порядку!
>
> ВЫ МОЖЕТЕ СЛОМАТЬ СВОЕ УСТРОЙСТВО С ПОМОЩЬЮ ПРИВЕДЕННЫХ НИЖЕ КОМАНД, ЕСЛИ БУДЕТЕ ВЫПОЛНЯТЬ ИХ НЕПРАВИЛЬНО!!!

### Открыть CMD от имени администратора
> Скачайте **platform-tools** и распакуйте его куда-нибудь, затем откройте CMD от имени **администратора**.
>
> Рекомендуется держать CMD открытым и использовать его на протяжении всего руководства.
> 
> Замените `путь\к\platform-tools` на путь к папке platform-tools, например **C:\platform-tools**.
```cmd
cd путь\к\platform-tools
```

> [!Note]
> If your device is not detected in fastboot or recovery mode, you'll have to install USB drivers [using this guide](troubleshooting-ru.md#device-is-not-recognized-in-fastboot-or-recovery)

#### Прошейте Модифицированный recovery
> Откройте окно CMD внутри папки platform-tools, затем (пока ваш телефон находится в режиме fastboot) выполните 
```cmd
fastboot flash recovery путь\к\modded-recovery-dipper.img reboot recovery
```

### Создание резервной копии важных файлов
> Это создаст бэкап **fsc**, **fsg**, **modemst1** и **modemst2** в текущем расположении, где открыта ваша командная строка (например **C:\platform-tools**). Убедитесь, что эти файлы действительно сдесь, прежде чем продолжить.
>
> Сохраните эти резервные копии в надежном месте. Если программное обеспечение вашего устройства однажды будет уничтожено, вам могут понадобиться эти резервные копии, иначе ваш телефон может потерять возможности сотовой связи.
>
> Если вы хотите создать резервную копию чего-либо ещё, сделайте это сейчас. Ваши данные в Android будут удалены в ходе следующих действий.
```cmd
cmd /c "for %i in (fsg,fsc,modemst1,modemst2) do (adb shell dd if=/dev/block/by-name/%i of=/tmp/%i.bin & adb pull /tmp/%i.bin)"
```

#### Бэкап вашего boot образа
> Это позволит создать резервную копию вашего текущего загрузочного образа в текущем каталоге.
```cmd
adb pull /dev/block/by-name/boot boot.img
```

### Разметка вашего устройства 
> Есть два метода чтобы разметить ваше устройство. Пожалуйста, выберите предпочитаемый метод ниже. 

#### Метод 1: Ручная разметка 

<details>
  <summary><strong>Нажмите здесь для метода 1</strong></summary> 

#### Размантируйте data
> Игнорируйте любые возможные ошибки и продолжайте
```cmd
adb shell umount /dev/block/by-name/userdata
```

#### Opening a shell
```cmd
adb shell
```

### Подгатовка к разметке
$${\color{lightblue}🟦 Note}$$
> If at any moment in parted you see an error prompting you to type "Yes/No" or "Ignore/Cancel", type `Yes` or `Ignore` depending on the situation to ignore the errors and continue.
>
> If you see any **udevadm** errors, you can ignore these as well.
```cmd
parted /dev/block/sda
```

#### Отобразить текущую таблицу разделов
> Parted выведет список разделов, userdata должна быть последним разделом в списке.
```cmd
print
```

#### Удалить userdata
> Замените **`$`** номером раздела **`userdata`**, должен быть **`21`**
```cmd
rm $
```

#### Заново создать userdata
> Замените **1611MB** с прежним начальным значением **userdata** который мы только что удалили (вероятно, это 1611МБ)
>
> Замените **32GB** с конечным значением, которое вы хотите, чтобы **userdata** имела. В этом примере ваша доступная используемая память в Android будет  32GB-1611MB = **30GB**
```cmd
mkpart userdata ext4 1611MB 32GB
```

#### Создать раздел ESP
> Замените **32GB** с конечным значением **userdata**
>
> Замените **32.3GB** тем значением, которое вы использовали ранее, добавив к нему **0.3GB**
```cmd
mkpart esp fat32 32GB 32.3GB
```

#### Создать раздел Windows
> Замените **32.3GB** с конечным значением **esp**
```cmd
mkpart win ntfs 32.3GB -0MB
```

#### Сделать ESP загрузочным
> Используйте `print` чтобы отобразиь все разделы. Замените `$` с вашим номером раздела ESP, который должен быть **`22`**
```cmd
set $ esp on
```

#### Выйти из parted
```cmd
quit
```

### Отформатировать data
- Отформатируйте все данные в TWRP, иначе Android не загрузится.
- (Перейдите к `Wipe` > `Format data` > напечатайте `yes`)

#### Проверьте, запускается ли Android 
- Просто перезагрузите телефон и посмотрите, загружается ли Android

### Форматирование дисков Windows и ESP
> Перезагрузитесь в модифицированное recovery, затем запустите эти две команды
```cmd
adb shell mkfs.ntfs -f /dev/block/by-name/win -L WINDIPPER
```

```cmd
adb shell mkfs.fat -F32 -s1 /dev/block/by-name/esp -n ESPDIPPER
```

### Fixing the GPT
> If you do not do this, Windows may break your device
```cmd
adb shell fixgpt
```

</details>

#### Метод 2: Автоматическая разметка

<details>
  <summary><strong>Нажмите здесь для метода 2</strong></summary> 

### Запустите скрипт разметки 
> After running the script, enter the size (in GB) that you want Windows to be
>
> Do not write **GB**, just the number (for example **50**)
```cmd
adb shell partition
``` 

### Проверьте, запускается ли Android 
- Просто перезагрузите телефон и посмотрите, загружается ли Android

</details>

## [Следующий шаг: Получение root прав](2-root-ru.md)





















