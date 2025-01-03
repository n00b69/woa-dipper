<img align="right" src="https://github.com/n00b69/woa-dipper/blob/main/dipper.png" width="350" alt="Windows 11 running on a Redmi K20 Pro">

# Running Windows on the Xiaomi Mi 8

## Reinstalling Windows without a PC

### Prerequisites
- A rooted Xiaomi Mi 8

- [Modified OFOX](https://github.com/n00b69/woa-dipper/releases/download/Files/modded-ofox-dipper.img)

- [Dipper WinInstaller](https://github.com/n00b69/woa-dipper/releases/download/Files/DipperWinInstaller.zip)

- [Windows on ARM image](https://arkt-7.github.io/woawin/)

- [WOA Helper app](https://github.com/n00b69/woa-helper/releases/tag/APK)

- Optional: a USB stick

### Preparing necessary files
- Download the Windows image and make sure it remains in the `Download` folder of your **internal storage**.
- Download **WinInstaller.zip** and keep it in the `Download` folder as well.

### Flash the modified OFOX
> If you have a custom recovery installed, you can install the modified OFOX through there instead
- Download the modified OFOX, rename it to **OFOX.img**, and leave in the `Download` folder **of your internal storage**.
- Download **Termux**, open it, and grant it root access.
- Run the below command in Termux to flash OFOX:
```cmd
su -c dd if=/sdcard/Download/OFOX.img of=/dev/block/by-name/recovery
```
- Run the below command in Termux to reboot into OFOX:
```cmd
su -c reboot recovery
```

#### Opening OFOX terminal
> Enter your password in OFOX, if it asks you to.
- Press the **Advanced** button on the bottom right of the screen, then press **Terminal**.

### Formatting Windows
```cmd
format
```

### Checking if decryption works
- Open the file explorer in OFOX, then navigate to your internal storage.
> If OFOX is not able to read/decrypt your internal storage, create a folder on your **USB stick** named `WOA` and put the **.esd** file and **WinInstaller.zip** in there instead
>
> Alternatively, find another OFOX image online that can actually decrypt and use it instead

### Flashing WinInstaller
- In OFOX, select **Install** and then locate **WinInstaller.zip** and flash it.
- Once you're given the option to reboot, do so.
> [!Note]
> Wait until all processes complete and your device boots into Windows. This will take around 15-20 minutes.

> [!Tip]
> If you wish to skip the Microsoft Account login, press the **I don't have internet** button in the WiFi page, then when prompted, press the **Continue with limited setup** button.

#### Booting to Android
- Run the **Android** shortcut on your desktop (you can also pin it to your start menu / taskbar for ease of access).

#### Booting to Windows
> If it says "UEFI NOT FOUND", download the [UEFI image](https://github.com/n00b69/woa-dipper/releases/tag/UEFI) and place it in the `UEFI` folder in your internal storage.
- Press **QUICKBOOT TO WINDOWS** inside the WOA Helper app, or use the newly created toggle in your quick settings panel.

## Finished!

























