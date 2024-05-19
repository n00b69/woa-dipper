<img align="right" src="https://github.com/n00b69/woa-dipper/blob/main/dipper.png" width="350" alt="Windows 11 running on dipper">

# Запуск Windows на Xiaomi Mi 8

## Разметка устройства 

### Требования 
- Мозг (самый важный из всех)

- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)
  
- [TWRP](https://github.com/n00b69/woa-dipper/releases/download/Files/twrp.img)

- [Parted](https://github.com/n00b69/woa-dipper/releases/download/Files/parted)

### Заметки 
> [!WARNING]  
> 
> НЕ ПЕРЕЗАГРУЖАЙТЕ ТЕЛЕФОН! Если вы считаете, что допустили ошибку, обратитесь за помощью в [Telegram чате](https://t.me/woadipper).
> 
> Не выполняйте все команды сразу, выполняйте их по порядку!
>
> ВЫ МОЖЕТЕ СЛОМАТЬ СВОЕ УСТРОЙСТВО С ПОМОЩЬЮ ПРИВЕДЕННЫХ НИЖЕ КОМАНД, ЕСЛИ БУДЕТЕ ВЫПОЛНЯТЬ ИХ НЕПРАВИЛЬНО!!!

#### Прошейте TWRP recovery
> Откройте окно CMD внутри папки platform-tools, затем (пока ваш телефон находится в режиме fastboot) выполните 
```cmd
fastboot flash recovery путь\к\twrp.img reboot recovery
```

#### Создание резервной копии важных файлов
> Это создаст бэкап **fsc**, **fsg**, **modemst1** и **modemst2** в текущем расположении, где открыта ваша командная строка (например **C:\platform-tools**). Убедитесь, что эти файлы действительно сдесь, прежде чем продолжить.
>
> Если вы хотите создать резервную копию чего-либо ещё, сделайте это сейчас. Ваши данные в Android будут удалены в ходе следующих действий.
```cmd
adb shell "dd if=/dev/block/by-name/fsc of=/tmp/fsc" || true && adb pull /tmp/fsc || true && adb shell "dd if=/dev/block/by-name/fsg of=/tmp/fsg" || true && adb pull /tmp/fsg || true && adb shell "dd if=/dev/block/by-name/modemst1 of=/tmp/modemst1" || true && adb pull /tmp/modemst1 || true && adb shell "dd if=/dev/block/by-name/modemst2 of=/tmp/modemst2" || true && adb pull /tmp/modemst2
```

### Руководство по разметке
> Ваш Xiaomi Mi 8 может иметь разный объем памяти. В данном руководстве в качестве примера используются значения для модели емкостью 128 ГБ. При необходимости в руководстве будет указано, можно или нужно ли использовать другие значения.

#### Размантируйте data
- Перейдите к `Монтировать` в TWRP и размонтируйте Data, если она смонтирована

#### Подгатовка к разметке 
> Скачайте файл parted и переместите его в папку platform-tools, затем запустите
```cmd
adb push parted /cache/ && adb shell "chmod 755 /cache/parted" && adb shell /cache/parted /dev/block/sda
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
> Замените **32GB** с конечным значением, которое вы хотите, чтобы **userdata** имела
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
>
> Замените **123GB** на конечное значение вашего диска, используйте `p free`, чтобы найти его
```cmd
mkpart win ntfs 32.3GB 123GB
```

#### Сделать ESP загрузочным
> Используйте `print` чтобы отобразиь все разделы. Замените `$` с вашим номером раздела ESP, который должен быть 22
```cmd
set $ esp on
```

#### Выйти из parted
```cmd
quit
```

#### Отформатировать data
- Отформатируйте все данные в TWRP, иначе Android не загрузится.
- (Перейдите к `Wipe` > `Format data` > напечатайте `yes`)

### Проверьте, запускается ли Android 
- Просто перезагрузите телефон и посмотрите, загружается ли Android


## [Следующий шаг: Установка Windows](2-install-ru.md)
