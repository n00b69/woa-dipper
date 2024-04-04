<img align="right" src="https://github.com/n00b69/woa-dipper/blob/main/dipper.png" width="350" alt="Windows 11 running on dipper">

# Running Windows on the Xiaomi Mi 8

## Dualboot guide

### Prerequisites
- [Magisk](https://github.com/topjohnwu/Magisk/releases/latest)

- [UEFI image](https://github.com/n00b69/woa-dipper/releases/tag/UEFI)

- [WOA Helper app](https://github.com/Marius586/WoA-Helper-update/releases/tag/WOA)

- [Switch To Android package](https://github.com/n00b69/woa-dipper/releases/download/Files/dipper-sta.zip)

## Dualboot guide
This guide assumes you are rooted, if you aren't, please follow [this guide](root.md) first.

### Setup - Android
- Download and install the WOA Helper app, then open it and grant it root access.
- Download the UEFI image and place it inside the folder named `UEFI` in your internal storage.
- Press the `Mount Windows` button to mount Windows to your internal storage at `/sdcard/Windows`
- Create a folder called `sta` in Windows and unpack the two files in the `Switch to Android package` file here (the files should go to `/sdcard/Windows/sta`
> [!Note]
> If the above step fails, press `flash UEFI` instead, then reboot to boot to Windows, press restart in Windows, then as it is restarting boot back to recovery to flash your Android boot.img located in your internal storage, and try again.
- Return to the WOA Helper app and press the `Quickboot` button.

### Setup - Windows
- Navigate to C:\sta and create a shortcut of `sta.exe` to your desktop.

#### Booting to Android
- Run the new shortcut on your desktop (you can also pin it to your start menu / taskbar for ease of access)

#### Booting to Windows
- Press `Quickboot to Windows` inside the app, or use the newly created toggle in your quick settings panel
  
## Finished!




















