<img align="right" src="https://github.com/n00b69/woa-dipper/blob/main/dipper.png" width="350" alt="Windows 11 running on dipper">

# Windows na Xiaomi Mi 8

## Tworzenie partycji

### Wymagania
- Mózg (najważniejsze ze wszystkich)

- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)
  
- [TWRP](https://github.com/n00b69/woa-dipper/releases/download/Files/twrp.img)

- [Parted](https://github.com/n00b69/woa-dipper/releases/download/Files/parted)

### Notes
> [!Warning]  
> 
> NIE URUCHAMIAJ PONOWNIE TELEFONU! Jeśli uważasz, że popełniłeś błąd, poproś o pomoc na [czacie telegramowym](https://t.me/woadipper).
> 
> Nie uruchamiaj wszystkich poleceń na raz, wykonuj je po kolei!
>
> MOŻESZ ZNISZCZYĆ SWOJE URZĄDZENIE ZA POMOCĄ PONIŻSZYCH POLECEŃ, JEŚLI ZROBISZ JE ŹLE!!!

#### Zflashuj TWRP
> Otwórz okno CMD w folderze platform-tools, a następnie (gdy telefon jest w trybie szybkiego uruchamiania) uruchom
```cmd
fastboot flash recovery path\to\twrp.img reboot recovery
```

#### Backing up important files
> This will back up **fsc**, **fsg**, **modemst1** and **modemst2** to the current path your CMD is opened in (for example **C:\platform-tools**). Confirm these files are actually there before proceeding.
>
> If you've got anything else you want to back up, do this now. Your Android data will be erased in the next steps.
```cmd
adb shell "dd if=/dev/block/by-name/fsc of=/tmp/fsc" || true && adb pull /tmp/fsc || true && adb shell "dd if=/dev/block/by-name/fsg of=/tmp/fsg" || true && adb pull /tmp/fsg || true && adb shell "dd if=/dev/block/by-name/modemst1 of=/tmp/modemst1" || true && adb pull /tmp/modemst1 || true && adb shell "dd if=/dev/block/by-name/modemst2 of=/tmp/modemst2" || true && adb pull /tmp/modemst2
```

### Przewodnik dotyczący partycjonowania
> Twój Xiaomi Mi 8 może mieć różne rozmiary pamięci. Ten przewodnik używa wartości modelu 128GB jako przykładu. W razie potrzeby przewodnik wspomni, czy można lub należy użyć innych wartości.

#### Odmontuj dane
- Przejdź do "Montuj" w TWRP i odmontuj dane, jeśli są zamontowane

#### Przygotowanie do partycjonowania
> Pobierz plik parted i przenieś go do folderu platform-tools, a następnie uruchom
```cmd
adb push parted /cache/ && adb shell "chmod 755 /cache/parted" && adb shell /cache/parted /dev/block/sda
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
> Zastąp **32GB** wartością końcową, jaką chcesz mieć dla **userdata**
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
>
> Zamień **123GB** na końcową wartość dysku, użyj `p free`, aby go znaleźć
```cmd
mkpart win ntfs 32.3GB 123GB
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

#### Formatowanie danych
- Sformatuj wszystkie dane w TWRP, w przeciwnym razie Android nie uruchomi się.
- (Idź do Wyczyść > Formatuj dane > wpisz yes)

#### Sprawdź, czy Android nadal się uruchamia
- Po prostu uruchom ponownie telefon i sprawdź, czy Android nadal działa


## [Następny Krok](2-install.md)





















