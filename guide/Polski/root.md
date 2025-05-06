<img align="right" src="https://github.com/n00b69/woa-dipper/blob/main/dipper.png" width="350" alt="Windows 11 running on dipper">

# Windows na Xiaomi Mi 8

## Przewodnik po rootowaniu

### Wymagania
- [Magisk](https://github.com/topjohnwu/Magisk/releases/latest)

- [ADB i Fastboot](https://developer.android.com/studio/releases/platform-tools)

- [Zmodyfikowane recovery](https://github.com/n00b69/woa-dipper/releases/tag/Recovery)

### Uruchom zmodyfikowane recovery
> Jeśli Twoje recovery zostało przywrócone do stanu fabrycznego, wykonaj flashowanie ponownie w trybie fastboot za pomocą:
```cmd
fastboot flash recovery path\to\modded-recoveey-dipper.img
```
#### Tworzenie kopii zapasowej obrazu rozruchowego
> Czasami flashowanie Magiska może spowodować bootloop. Aby to naprawić, musisz przywrócić kopię zapasową pliku boot.img.

Użyj funkcji tworzenia kopii zapasowych TWRP, aby utworzyć kopię zapasową partycji rozruchowej.

#### Flashowanie Magiska
- Zflashuj plik magisk.apk (być może będziesz musiał zmienić jego nazwę na magisk.zip) i zrestartuj telefon.
- Po uruchomieniu zlokalizuj aplikację Magisk i otwórz ją.
- Postępuj zgodnie z otrzymanymi instrukcjami. Wybierz metodę instalacji bezpośredniej, jeśli dostępnych jest kilka metod.

Twój telefon uruchomi się ponownie i pomyślnie go zrootowałeś.

> [!Important]
> Po zrootowaniu telefonu utwórz nową kopię zapasową pliku boot.img w systemie Android i Windows (za pomocą aplikacji WOA Helper) i usuń wszelkie pozostałe utworzone wcześniej kopie zapasowe pliku boot.img. Jeśli tego nie zrobisz, przejście na Androida spowoduje zrestartowanie telefonu.
>
> Po aktualizacji lub zmianie ROMu (i ponownym uruchomieniu) będziesz musiał powtórzyć wszystkie kroki opisane na tej stronie.

## Skończone!
