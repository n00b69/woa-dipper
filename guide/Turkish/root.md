<img align="right" src="https://github.com/n00b69/woa-dipper/blob/main/dipper.png" width="350" alt="Windows 11 running on dipper">

# Mi 8'de Windows çalıştırma

## Kök rehberi

### Gerekli olanlar
- [Magisk](https://github.com/topjohnwu/Magisk/releases/latest)

- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)

- [TWRP](https://github.com/n00b69/woa-dipper/releases/download/Files/twrp.img)

### TWRP'ye gir
> Eğer recovery'niz stock olarak değiştirildiyse, fastboot ile tekrar flashlayın:
``cmd
fastboot flash recovery path\to\twrp.img reboot recovery```

#### Önyükleme görüntünüzü yedekleme
> Bazen Magisk'in yanıp sönmesi bir bootloop'a neden olabilir. Bunu düzeltmek için bir boot.img yedeğini geri yüklemeniz gerekir.

Önyükleme bölümünün yedeğini almak için TWRP yedekleme özelliğini kullanın.

### Magisk Yükleme
- Magisk.apk dosyasını flash'layın (magisk.zip olarak yeniden adlandırmanız gerekebilir) ve telefonunuzu yeniden başlatın. 
- Önyüklendikten sonra Magisk uygulamasını bulun ve açın.
- Sağlanan tüm talimatları izleyin. Size birkaç yöntem sunulursa doğrudan yükleme yöntemini seçin.

Telefonunuz şimdi yeniden başlatılacak ve başarılı bir şekilde root atmış olacaksınız.

> [!ÖNEMLİ]
> Telefonunuzu rootladıktan sonra, Android'de ve Windows'ta (WOA Helper uygulamasını kullanarak) yeni bir boot.img yedeği oluşturun ve daha önce yaptığınız tüm boot.img yedeklerini kaldırın. Bunu yapmazsanız, Android'e geçmek telefonunuzun root'unu kaldıracaktır.
> 
> Romunuzu güncelledikten veya değiştirdikten (ve yeniden rootlamak) sonra bu sayfadaki tüm adımları tekrarlamanız gerekecektir.

## Bitti!
