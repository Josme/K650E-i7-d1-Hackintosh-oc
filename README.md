# Hackintosh-big-sur-hasee-k650E-i7-d1

## 电脑配置

| 规格  | 详细信息     |
| ---- | ----------  |
| CPU | Intel Haswell i7-4710MQ |
| 显卡 | Intel HD Graphics 4600 + NVIDIA GeForce GTX 950M（已屏蔽） |
| 声卡 | VIA VT1802P |
| 网卡 | RealtekRTL8111 + AR5B125（已更换 BCM94352HMB） |
| 硬盘 | Micron_M_510 128GB + Colorful SL500 1TB |

## 硬件驱动情况
- **显卡**：正常，必须屏蔽独显，日常使用核显hd4600足够了，*ig-platform-id*为`0x0a260006`,仿冒*device-id*为`0x12040000`,结合WhateverGreen使用WEG自定义补丁修复显存 花屏及HDMI等，开机8苹果及花屏请先外接显示器然后调整显示器分辨率1600*900.
- **声卡**：使用AppleALC仿冒Apple内建声卡，配置*layout-id*为`3`
- **有线网卡**：使用RealtekRTL8111.kext驱动就可以了
- **无线网卡+蓝牙**：自带网卡无法驱动，更换为Mini pci-e接口的*博通 BCM94352HMB*，需要用胶带屏蔽51针脚以及USB端口定制（蓝牙模块走usb总线），使用AirportBrcmFixup+BrcmFirmwareData+BrcmPatchRAM3+BrcmBluetoothInjector驱动，可完美使用AirDrop HandOff SideCar等
- **睡眠+休眠**：不正常
- **SSDT**：CPU变频正常
- **USB**：正常
- **内置键盘+触控板**：使用ApplePS2SmartTouchPad驱动

- **内置键盘command和option键错位**：使用[Karabiner](https://pqrs.org/osx/karabiner/)软件更改按键映射
- **无法正常使用键盘上的home+end等键**：使用*Karabiner*或者在终端里输入以下命令保存文件重启电脑
    ```
    $ cd ~/Library
    $ mkdir KeyBindings
    $ cd KeyBindings
    $ vim DefaultKeyBinding.dict
    {
    /* Remap Home / End keys to be correct */
    "\UF729" = "moveToBeginningOfLine:"; /* Home */
    "\UF72B" = "moveToEndOfLine:"; /* End */
    "$\UF729" = "moveToBeginningOfLineAndModifySelection:"; /* Shift + Home */
    "$\UF72B" = "moveToEndOfLineAndModifySelection:"; /* Shift + End */
    "^\UF729" = "moveToBeginningOfDocument:"; /* Ctrl + Home */
    "^\UF72B" = "moveToEndOfDocument:"; /* Ctrl + End */
    "$^\UF729" = "moveToBeginningOfDocumentAndModifySelection:"; /* Shift + Ctrl + Home */
    "$^\UF72B" = "moveToEndOfDocumentAndModifySelection:"; /* Shift + Ctrl + End */
    }
    ```
