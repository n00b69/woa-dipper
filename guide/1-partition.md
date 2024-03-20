<img align="right" src="https://github.com/n00b69/woaenchilada/blob/main/enchilada.png" width="350" alt="Windows 11 running on enchilada">

# Running Windows on the OnePlus 6

## Partitioning your device

### Prerequisites
- A brain (most important of all)

- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)
  
- [TWRP]() FILE NEEDED

- [Parted](https://github.com/n00b69/woapolaris/releases/download/Files/parted)

### Notes
> [!WARNING]  
> If you ever delete any partitions via diskpart, Windows will send a UFS command which would erase the entire UFS storage!
> 
> All your data will be erased! Back up now if needed.
> 
> Do not run the same command twice unless specified.
> 
> DO NOT REBOOT YOUR PHONE! If you think you made a mistake, ask for help in the [Telegram chat](https://t.me/WinOnF1).
> 
> Do not run all commands at once, execute them in order!
>
> YOU CAN BREAK YOUR DEVICE WITH THE COMMANDS BELOW IF YOU DO THEM WRONG!!!

#### Flash TWRP recovery
> Open a CMD window inside the platform-tools folder, then (while your phone is in fastboot mode) run
```cmd
fastboot flash recovery path\to\twrp.img reboot recovery
```

> [!IMPORTANT]
> If you do anything incorrectly, you may wipe your UFS and render your device unusable.

Use TWRP now to back up your Modem and EFS partition (as well as anything else if you have important data). Move this backup to a safe place (e.g your PC) as the next steps will wipe your data.

#### Partitioning guide
> Your Xiaomi Mix 2s may have different storage sizes. This guide uses the values of the 128GB model as an example. When relevant, the guide will mention if other values can or should be used.

#### Preparing for partitioning
> Download the parted file and move it in the platform-tools folder, then run
```cmd
adb push parted /cache/ && adb shell "chmod 755 /cache/parted" && adb shell /cache/parted /dev/block/sda
```

#### Printing the current table partition:
> Parted will print the list of partitions, userdata should be the last partition in the list.
```cmd
print
```

#### Resizing userdata
> Replace $ with the number of the userdata partition, which should be 21
>
> If it asks you if you are okay with data loss, type yes
```cmd
resizepart $
```
> Parted will now ask you for the end value.
> You can choose the size you want, as long as it is lower than the value it provides to you. In this example we resize it to 32GB
```cmd
End? [123GB]? 32GB
```
Note: 123GB is parted telling us the maximum end value we can select.

#### Checking free space
```cmd
p free
```

#### Creating Windows partition
> In this example, 122.5GB is the **End** of the **Windows** partition we will be creating. Replace "122.5GB" with your actual end value, making sure to subtract 0.5GB which will be used to create the ESP partition

> 32GB in this example is the end of userdata, replace this with your actual end value accordingly as well
```cmd
mkpart win ntfs 32GB 122.5GB
```

#### Creating ESP partition
> 122.5GB is the **End** of the **Windows** partition in this example and 123GB is the end of the ESP partition we will be creating, which will be 500MB in size

> Replace 122.5GB with the actual value you used when resizing the partition, then add 0.5 to this value and use it for the second value
```cmd
mkpart esp fat32 122.5GB 123GB
```

#### Making ESP bootable
> Replace $ with the actual number of the ESP partition which you can get using the `print` command, which should be 23
```cmd
set $ esp on
```

#### Exit parted
```cmd
quit
```

#### Formatting data
- Format all data in TWRP, or Android will not boot.
- ( Go to Wipe > Format data > type yes )

#### Check if Android still starts
- Just restart the phone, and see if Android still works


## [Next step: Installing Windows](/guide/2-install.md)




















