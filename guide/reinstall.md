<img align="right" src="https://github.com/n00b69/woa-dipper/blob/main/dipper.png" width="350" alt="Windows 11 running on dipper">

# Running Windows on the Xiaomi Mi 8

## Reinstalling Windows

### Prerequisites
- [Windows on ARM image](https://worproject.com/esd)

- [Drivers](https://github.com/n00b69/woa-dipper/releases/tag/Drivers)

- [Devcfg (touch fix)](https://github.com/n00b69/woa-dipper/releases/download/Files/devcfg-dipper.img)

- [UEFI image](https://github.com/n00b69/woa-dipper/releases/tag/UEFI)

### Boot to the UEFI
> Replace **<path\to\dipper-uefi.img>** with the actual path of the UEFI image
```cmd
fastboot boot <path\to\dipper-uefi.img>
```

#### Enabling mass storage mode
> Once booted into the UEFI, use the volume buttons to navigate the menu and the power button to confirm
- Select **UEFI Boot Menu**.
- Select **USB Attached SCSI (UAS) Storage**.
- Press the **power** button twice to confirm.

### Diskpart
```cmd
diskpart
```

### List device volumes
> To print a list of all the connected volumes, run
```cmd
list volume
```

#### Select Windows volume
> Replace $ with the actual number of **WINDIPPER**
```cmd
select volume $
```

#### Add letter to Windows
```cmd
assign letter x
```

#### Exit diskpart
```cmd
exit
```

#### Formatting Windows
> Go to Windows Exlorer > This PC and select **WINDIPPER**. Right click and format as NTFS.

### Installing Windows
> Replace `<path\to\install.esd>` with the actual path of install.esd (it may also be named install.wim)
```cmd
dism /apply-image /ImageFile:<path\to\install.esd> /index:6 /ApplyDir:X:\
```

> If you get `Error 87`, check the index of your image with `dism /get-imageinfo /ImageFile:<path\to\install.esd>`, then replace `index:6` with the actual index number of Windows 11 Pro in your image

### Installing Drivers
> Extract the drivers folder from the archive, then run the following command, replacing`<path\to\drivers>` with the actual path of the drivers folder
```cmd
dism /image:X:\ /add-driver /driver:<path\to\drivers> /recurse
```

### Reboot to fastboot
> Hold the **volume up** + **power** button until it boots to fastboot

### Fixing touch
> Replace "path\to" with the actual path to the image
```cmd
fastboot flash devcfg_ab path\to\devcgf-dipper.img
```

### Boot into Windows
Reboot your phone. If you end up in Android instead of Windows, flash the UEFI again using WOA Helper.

#### Setting up Windows
> Your device will now set up Windows. This will take some time. It will eventually reboot, and after that the initial setup (oobe) should launch.

> [!Note]
> To skip the Microsoft Account login, use "g" for the email and password. Windows will then let you make a local account

## Finished!
















