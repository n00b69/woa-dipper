<img align="right" src="https://github.com/n00b69/woa-dipper/blob/main/dipper.png" width="350" alt="Windows 11 running on dipper">

# Windows na Xiaomi Mi 8

## Aktualizowanie sterowników

### Wymagania
- [ADB i Fastboot](https://developer.android.com/studio/releases/platform-tools)
  
- [Sterowniki](https://github.com/n00b69/woa-dipper/releases/tag/Drivers)

- [Obraz UEFI](https://github.com/n00b69/woa-dipper/releases/tag/UEFI)

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
```cmd
diskpart
```

#### Wybór partycji Windows
> Użyj `list Volume`, aby go znaleźć, zamień `$` na rzeczywistą liczbę **WINDIPPER**
```diskpart
select volume $
```

#### Dodaj literę do systemu Windows
```cmd
assign letter x
```

#### Wyjdź z Diskpart
```cmd
exit
```

### Instalowanie sterowników
> [!Note]
> Ten proces zajmie +- 20 minut. Nie martw się, to normalne.

- Wypakuj archiwum ze sterownikami, potem otwórz plik `OfflineUpdater.cmd` (jeśli pojawi się błąd, otwórz `OfflineUpdaterFix.cmd`)
 
> Jeśli poprosi cię o podanie litery, wpisz literę dysku **WINDIPPER** (która powinna być **X**), a następnie naciśnij enter.

### Uruchom ponownie urządzenie
> Pamiętaj, aby zmienić także obraz UEFI w systemie Android, w przeciwnym razie podczas późniejszego uruchamiania systemu Windows może pojawić się „niebieski ekran śmierci” (BSoD).
```cmd
adb reboot
```

## Skończone!















