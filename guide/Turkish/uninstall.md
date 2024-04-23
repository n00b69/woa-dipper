<img align="right" src="https://github.com/n00b69/woa-dipper/blob/main/dipper.png" width="350" alt="Windows 11 running on dipper">

# Mi 8'de Windows çalıştırma

## Kaldırma

### Bu neden gerekli?
Eğer windows'u kaldırmak istiyorsanız, bu, insan hatasını önlemek için bölümleri manuel olarak silmek yerine kullanılır + sadece kaldırmak için bir rehber yazmayıda önlüyor.

Önyükleyicinizi yeniden kilitlemek istiyorsanız, bölümleme tablonuzun stok (fabrika çıkışı) olması gerekir.

### Gerekli olanlar

- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)
  
- [gpt_both0.bin](https://github.com/n00b69/woa-dipper/releases/download/Files/gpt_both0.bin)

#### Fastboot'a gir
> Telefon kapalı iken ses kısma + güç düğmesine basılı tutun, ya da telefon çalışırken:
```cmd
adb reboot bootloader
```

#### GPT'yi restore etmek
> Bunu```C:\Users\kullaniciadin\Downloads\gpt_both0.bin``` gpt_both0.bin dosyasının bulunduğu konumla değiştirin 

```cmd
fastboot flash partition:0 C:\Users\kullaniciadin\Downloads\gpt_both0.bin
```

#### Bootloop'u önlemek için userdata'yı sil ve FS boyutuna restore et
```cmd
fastboot -w
```
> [!Note]
> Eğer userdata'yı silerken hata ile karşılaştıysan, kurtarma bölümüne girip ordan silmeniz gerekebilir.

## Bitti

