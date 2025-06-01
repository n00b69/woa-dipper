<img align="right" src="https://github.com/n00b69/woa-dipper/blob/main/dipper.png" width="350" alt="Windows 11 running on dipper">

# Windows na Xiaomi Mi 8

## Tworzenie partycji

### Wymagania
- Odblokowany bootloader

- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)
  
- [Zmodyfikowane recovery](https://github.com/n00b69/woa-dipper/releases/tag/Recovery)

### Uwagi
> [!Warning]  
> 
> NIE URUCHAMIAJ PONOWNIE TELEFONU! Jeśli uważasz, że popełniłeś błąd, poproś o pomoc na [Telegramie](https://t.me/woadipper).
> 
> Nie uruchamiaj wszystkich poleceń na raz, wykonuj je po kolei!
>
> MOŻESZ ZNISZCZYĆ SWOJE URZĄDZENIE ZA POMOCĄ PONIŻSZYCH POLECEŃ, JEŚLI ZROBISZ JE ŹLE!!!

### Otwieranie CMD jako administrator
> Pobierz **platform-tools** i wypakuj gdzieś folder, a następnie otwórz CMD jako **administrator**.
>
> Zaleca się pozostawienie tego okna otwartego i korzystanie z niego przez cały przewodnik.
> 
> Zastąp `ścieżka\do\platform-tools` rzeczywistą ścieżką do folderu platform-tools, na przykład **C:\platform-tools**.
```cmd
cd ścieżka\do\platform-tools
```

> [!Note]
> If your device is not detected in fastboot or recovery mode, you'll have to install USB drivers [using this guide](troubleshooting.md#device-is-not-recognized-in-fastboot-or-recovery)

#### Flashuj zmodyfikowane recovery
> Otwórz okno CMD w folderze platform-tools, a następnie (gdy telefon jest w trybie fastboot) wpisz
```cmd
fastboot flash recovery ścieżka\do\modded-recovery-dipper.img reboot recovery
```

### Tworzenie kopii zapasowej ważnych plików
> Spowoduje to utworzenie kopii zapasowej plików **fsc**, **fsg**, **modemst1** i **modemst2** w bieżącej ścieżce, w której otwarto CMD (na przykład **C:\platform-tools**). Przed kontynuowaniem upewnij się, że te pliki rzeczywiście tam są.
> 
> Trzymaj tę kopię zapasową w bezpiecznym miejscu. Jeśli oprogramowanie Twojego urządzenia kiedykolwiek ulegnie uszkodzeniu, możesz potrzebować tej kopii, gdyż w przeciwnym wypadku telefon może już nigdy nie być w stanie wykonywać połączeń.
> 
> Jeśli chcesz utworzyć kopię zapasową czegoś innego, zrób to teraz. Twoje dane Androida zostaną usunięte w kolejnych krokach.
```cmd
cmd /c "for %i in (fsg,fsc,modemst1,modemst2) do (adb shell dd if=/dev/block/by-name/%i of=/tmp/%i.bin & adb pull /tmp/%i.bin)"
```

#### Tworzenie kopii zapasowych obrazu rozruchu
> Spowoduje to utworzenie kopii zapasowej obecnego obrazu rozruchu w bieżącej ścieżce
```cmd
adb pull /dev/block/by-name/boot boot.img
```

### Przewodnik dotyczący partycjonowania
> There are two methods to partition your device. Please select the method you would like to use below. 

#### Method 1: Manual partitioning 

<details>
  <summary><strong>Click here for method 1</strong></summary> 

#### Odmontuj dane
> Ignore any possible errors and continue
```cmd
adb shell umount /dev/block/by-name/userdata
``` 

#### Opening a shell
```cmd
adb shell
```

### Przygotowanie do partycjonowania
$${\color{lightblue}🟦 Note}$$
> If at any moment in parted you see an error prompting you to type "Yes/No" or "Ignore/Cancel", type `Yes` or `Ignore` depending on the situation to ignore the errors and continue.
>
> If you see any **udevadm** errors, you can ignore these as well.
```cmd
parted /dev/block/sda
```

#### Wyświetlanie aktualnej tablicy partycji
> Parted wyświetli listę partycji, "userdata" powinenen być ostatnią partycją na liście.
```cmd
print
``` 

#### Usuwanie userdata
> Zamień **$** na numer partycji **userdata**, który powinien wynosić **21**
```cmd
rm $
``` 

#### Ponowne utworzenie userdata
> Zamień **1611MB** na poprzednią wartość początkową **userdata**, którą właśnie usunęliśmy (prawdopodobnie jest to 1611MB)
>
> Zastąp **32GB** wartością końcową, jaką chcesz mieć dla **userdata**. In this example your available usable space in Android will be 32GB-1611MB = **30GB**
```cmd
mkpart userdata ext4 1611MB 32GB
``` 

#### Tworzenie partycji ESP 
> Zamień **32GB** na końcową wartość **userdata**
>
> Zastąp **32.3GB** wartością, której użyłeś wcześniej, dodając do niej **0.3GB**
```cmd
mkpart esp fat32 32GB 32.3GB
``` 

#### Tworzenie partycji Windows
> Zastąp **32.3GB** wartością końcową **esp**
```cmd
mkpart win ntfs 32.3GB -0MB
``` 

#### Tworzenie bootowalnego ESP
> Użyj `print`, aby zobaczyć wszystkie partycje. Zamień „$” na numer partycji ESP, który powinien wynosić 22
```cmd
set $ esp on
``` 

#### Wyjdź z parted
```cmd
quit
``` 

### Formatowanie danych
- Sformatuj wszystkie dane w recovery, w przeciwnym razie Android nie uruchomi się.
- (Idź do Wyczyść > Formatuj dane > wpisz yes) 

#### Sprawdź, czy Android nadal się uruchamia
- Po prostu uruchom ponownie telefon i sprawdź, czy Android nadal działa 

### Formatting Windows and ESP drives
> Reboot into the modded recovery, then run the below two commands
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

#### Method 2: Automatic partitioning 

<details>
  <summary><strong>Click here for method 2</strong></summary>

### Uruchom skrypt partycjonowania
> After running the script, enter the size (in GB) that you want Windows to be
>
> Do not write **GB**, just the number (for example **50**)
```cmd
adb shell partition
``` 

#### Sprawdź, czy Android nadal się uruchamia
- Po prostu uruchom ponownie telefon i sprawdź, czy Android nadal działa

</details>

## [Następny krok: Rootowanie telefonu](2-root.md)





















