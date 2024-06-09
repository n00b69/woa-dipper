<img align="right" src="https://github.com/n00b69/woa-dipper/blob/main/dipper.png" width="350" alt="Windows 11 running on dipper">

# Running Windows on the Xiaomi Mi 8

## Installing Windows

### Prerequisites
- [Windows on ARM image](https://worproject.com/esd)
  
- [Drivers](https://github.com/n00b69/woa-dipper/releases/tag/Drivers)

- [Devcfg (touch fix)](https://github.com/n00b69/woa-dipper/releases/download/Files/devcfg-dipper.img)

- [UEFI image](https://github.com/n00b69/woa-dipper/releases/tag/UEFI)

### Boot to the UEFI
> Replace **path\to\dipper-uefi.img** with the actual path of the UEFI image
```cmd
fastboot boot path\to\dipper-uefi.img
```

#### Enabling mass storage mode
> Once booted into the UEFI, use the volume buttons to navigate the menu and the power button to confirm
- Select **UEFI Boot Menu**.
- Select **USB Attached SCSI (UAS) Storage**.
- Press the **power** button twice to confirm.

### Diskpart
> [!WARNING]
> DO NOT ERASE, CREATE OR OTHERWISE MODIFY ANY PARTITION WHILE IN DISKPART!!!! THIS CAN ERASE ALL OF YOUR UFS OR PREVENT YOU FROM BOOTING TO FASTBOOT!!!! THIS MEANS THAT YOUR DEVICE WILL BE PERMANENTLY BRICKED WITH NO SOLUTION! (except for flashing it with EDL)

```cmd
diskpart
```

#### Finding your phone
> This will list all connected disks
```cmd
lis dis
```

#### Selecting your phone
> Replace $ with the actual number of your phone (it should be the last one)
```cmd
sel dis $
```

#### Listing your phone's partitions
> This will list your device's partitions
```cmd
lis par
```

#### Selecting the Windows partition
> Replace $ with the partition number of Windows (should be 23)
```cmd
sel par $
```

#### Formatting Windows drive
```cmd
format quick fs=ntfs label="WINDIPPER"
```

#### Add letter to Windows
```cmd
assign letter x
```

#### Selecting the ESP partition
> Replace $ with the partition number of ESP (should be 22)
```cmd
sel par $
```

#### Formatting ESP drive
```cmd
format quick fs=fat32 label="ESPDIPPER"
```

#### Add letter to ESP
```cmd
assign letter y
```

#### Exit diskpart
```cmd
exit
```

### Installing Windows
> Replace `path\to\install.esd` with the actual path of install.esd (it may also be named install.wim)

```cmd
dism /apply-image /ImageFile:path\to\install.esd /index:6 /ApplyDir:X:\
```

> If you get `Error 87`, check the index of your image with `dism /get-imageinfo /ImageFile:path\to\install.esd`, then replace `index:6` with the actual index number of **Windows 11 Pro** in your image

### Installing Drivers
> Unpack the driver archive, then open the `OfflineUpdater.cmd` file

> If it asks you to enter a letter, enter the drive letter of **WINDIPPER** (which should be **X**), then press enter
  
#### Create Windows bootloader files
```cmd
bcdboot X:\Windows /s Y: /f UEFI
```

#### Enabling test signing
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" testsigning on
```

#### Disabling recovery
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" recoveryenabled no
```

#### Disabling integrity checks
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" nointegritychecks on
```

### Unassign disk letters
> So that they don't stay there after disconnecting the device
```cmd
diskpart
```

#### Select the Windows volume of the phone
> Use `list volume` to find it, replace "$" with the actual number of **WINDIPPER**
```diskpart
select volume $
```

#### Unassign the letter X
```diskpart
remove letter x
```

#### Select the ESP volume of the phone
> Use `list volume` to find it, replace "$" with the actual number of **ESPDIPPER**
```diskpart
select volume $
```

#### Unassign the letter Y
```diskpart
remove letter y
```

#### Exit diskpart
```diskpart
exit
```

### Reboot to fastboot
```cmd
adb reboot bootloader
```

### Fixing touch
> Replace **path\to** with the actual path to the image
```cmd
fastboot flash devcfg_ab path\to\devcgf-dipper.img
```

### Reboot to Android
> To set up dualboot
```cmd
fastboot reboot
```

## [Last step: Setting up dualboot](/guide/dualboot.md)

















