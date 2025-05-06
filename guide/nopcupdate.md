<img align="right" src="https://github.com/n00b69/woa-dipper/blob/main/dipper.png" width="350" alt="Windows 11 running on a Redmi K20 Pro">

# Running Windows on the Xiaomi Mi 8

## Updating drivers without a PC

### Prerequisites
- A rooted Xiaomi Mi 8

- [Modded recovery](https://github.com/n00b69/woa-dipper/releases/tag/Recovery)

- [Dipper WinInstaller](https://github.com/n00b69/woa-dipper/releases/download/Files/DipperWinInstaller.zip)

### Notes
> [!WARNING]  
> 
> DO NOT REBOOT YOUR PHONE if you think you made a mistake, ask for help in the [Telegram chat](https://t.me/woadipper).

> [!Important]
> This guide assumes you have already installed Windows. If you haven't, use the [installation guide](nopc.md) instead.

### Preparing necessary files
- Download **WinInstaller.zip** and keep it in your **internal storage** or put it on your **USB stick**.

### Flash the modified recovery
> If you already have a recovery with decryption support, you can skip this step
- Download the modified recovery, rename it to **recovery.img**, and leave in the `Download` folder **of your internal storage**.
- Download **Termux**, open it, and grant it root access.
- Run the below command in Termux to flash the modified recovery:
```cmd
su -c dd if=/sdcard/Download/recovery.img of=/dev/block/by-name/recovery
```
- Run the below command in Termux to reboot into the modified recovery:
```cmd
su -c reboot recovery
```

### Flashing WinInstaller
- In the recovery, select **Install** and then locate **WinInstaller.zip** and flash it.
- Once you're given the option to reboot, do so.
> [!Note]
> Wait until all processes complete and your device boots back into Windows. This will take around 20-30 minutes.

## Finished!
































