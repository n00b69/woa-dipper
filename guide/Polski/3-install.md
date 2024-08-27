<img align="right" src="https://github.com/n00b69/woa-dipper/blob/main/dipper.png" width="350" alt="Windows 11 running on dipper">

# Windows na Xiaomi Mi 8

## Instalacja Windowsa

### Wymagania
- [Obraz UEFI](https://github.com/n00b69/woa-dipper/releases/tag/UEFI)

- [Windows na ARM](https://arkt-7.github.io/woawin/)
  
- [Sterowniki](https://github.com/n00b69/woa-dipper/releases/tag/Drivers)

- [Devcfg (naprawia dotyk)](https://github.com/n00b69/woa-dipper/releases/download/Files/devcfg-dipper.img)

### Uruchom do UEFI
> Zastąp `ścieżka\do\dipper-uefi.img` rzeczywistą ścieżką obrazu UEFI
```cmd
fastboot boot ścieżka\do\dipper-uefi.img
```

#### Włączanie trybu pamięci masowej
> Po uruchomieniu systemu UEFI użyj przycisków głośności do poruszania się po menu i przycisku zasilania, aby potwierdzić
- Wybierz **UEFI Boot Menu**.
- Wybierz **USB Attached SCSI (UAS) Storage**.
- Naciśnij przycisk dwa razy aby potwierdzić.

### Diskpart
> [!WARNING]
> NIE USUWAJ ŻADNYCH PARTYCJI W DISKPART!!!! TO USUNIE CAŁĄ ZAWARTOŚĆ PAMIĘCI!!!! OZNACZA TO, ŻE TWOJE URZĄDZENIE ZOSTANIE TRWALE USZKODZONE BEZ ROZWIĄZANIA! (z wyjątkiem wysłania go do Xiaomi lub flashowania go za pomocą EDL)
```cmd
diskpart
```

#### Wybieranie partycji Windows
> Wpisz `list Volume`, aby ją znaleźć, zamień `$` na rzeczywistą liczbę **WINDIPPER**
```diskpart
select volume $
```

#### Dodanie litery do systemu Windows
```cmd
assign letter x
```

#### Wybieranie partycji ESP
> Użyj `list Volume`, aby go znaleźć, zamień `$` na rzeczywistą liczbę **ESPDIPPER**
```diskpart
select volume $
```

#### Dodanie literę do ESP
```cmd
assign letter y
```

#### Wyjście z Diskpart
```cmd
exit
```

### Instalowanie Windowsa
> [!WARNING]
> NIE UŻYWAJ 24H2!!!

> Zamień `ścieżka\do\install.esd` na rzeczywistą ścieżkę do pliku install.esd (może on również nosić nazwę install.wim lub 22631.2861.XXXXXXX.esd)
```cmd
dism /apply-image /ImageFile:ścieżka\do\install.esd /index:6 /ApplyDir:X:\
```

> Jeśli pojawi się komunikat `Błąd 87`, sprawdź indeks obrazu za pomocą polecenia `dism /get-imageinfo /ImageFile:ścieżka\do\install.esd`, a następnie zastąp `index:6` rzeczywistym numerem indeksu systemu **Windows 11 Pro** w Twoim obrazie

### Kopiowanie obrazu rozruchu do Windowsa
- Zaznacz i upuść **rooted_boot.img** z poprzedniego kroku do **WINDIPPER** w eksploratorze plików, a następnie zmień mu nazwę na **boot.img**.

### Instalowanie sterowników
- Wypakuj archiwum ze sterownikami, a następnie otwórz plik `OfflineUpdater.cmd` (jeśli pojawi się błąd, otwórz `OfflineUpdaterFix.cmd`)
 
> Jeśli poprosi Cię o podanie litery, wpisz literę dysku **WINDIPPER** (którą powinna być **X**), a następnie naciśnij enter.

#### Tworzenie plików bootloadera systemu Windows
```cmd
bcdboot X:\Windows /s Y: /f UEFI
```

#### Włączanie trybu testowego
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" testsigning on
```

#### Wyłączanie odzyskiwania
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" recoveryenabled no
```

#### Wyłączanie sprawdzania integralności
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" nointegritychecks on
```

#### Remove the drive letter for ESP
> If this does not work, ignore it and skip to the next command. This phantom drive will disappear the next time you reboot your PC.
```cmd
mountvol y: /d
```

### Uruchamianie ponownie w trybie fastboot
> Przytrzymaj **zmniejszanie głośności** + **zasilanie**, aby wymusić ponowne uruchomienie telefonu w trybie fastboot

### Naprawianie dotyku
> Zastąp `ścieżka\do\devcfg-dipper.img` rzeczywistą ścieżką obrazu
```cmd
fastboot flash devcfg_ab ścieżka\do\devcfg-dipper.img
```

#### Uruchamianie do UEFI
> Zastąp `ścieżka\do\dipper-uefi.img` rzeczywistą ścieżką obrazu UEFI
```cmd
fastboot boot ścieżka\do\dipper-uefi.img
```

### Uruchamianie ponownie do Androida
Telefon powinien uruchomić się ponownie sam po +- 10 minutach czekania, po których uruchomi się Android, aby wykonać ostatni krok.

## [Ostatni krok: Konfiguracja dualboot](4-dualboot.md)

















