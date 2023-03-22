# dkms-hid-nintendolic

A kernel module for the Nintendo Licensed pro-controller by Hori.

![image](https://user-images.githubusercontent.com/4388859/226704191-fa25b50f-6b8e-4e39-9f54-60c813d5e02a.png)

This is a (slightly) modified version of the [driver for the original Nintendo pro-controller](https://github.com/DanielOgorchock/linux).

## Detection

type `sudo dmesg` after connecting the controller via bluetooth or usb, you should get something like
```
[ 1375.472751] input: Lic Pro Controller as /devices/virtual/misc/uhid/0005:0F0D:00F6.0003/input/input23
```
Where
`0F0D` is the vendor ID
`00F6` is the model ID

In alternative, you can get the same IDs by `lsusb` after connecting via usb:
```
Bus 001 Device 051: ID 0f0d:00f6 Hori Co., Ltd HORI Wireless Switch Pad
```

## Installation

Install it from source with:

```
git clone https://github.com/cipitaua/dkms-hid-nintendolic
cd dkms-hid-nintendolic

sudo dkms add .
sudo dkms build nintendolic -v 3.2
sudo dkms install nintendolic -v 3.2
```

## Features

- almost everything works, including gyroscope

## Known issues

- rumble is not working
- screenshot button may not work, depending on the app

## SDL

- to map the xpad buttons through SDL, put the following in `/etc/profile.d/sdl2-gamecontroller.sh`, and reboot:
```
#!/bin/bash
# Creates a system-wide SDL2 mapping for any device that mimics xpad.
export SDL_GAMECONTROLLERCONFIG="050000000d0f0000f6000000018000003853246,Nintendo Switch Pro Controller,platform:Linux,a:b0,b:b1,x:b2,y:b3,back:b9,start:b10,guide:b11,leftshoulder:b5,rightshoulder:b6,leftstick:b12,rightstick:b13,leftx:a0,lefty:a1,rightx:a2,righty:a3,lefttrigger:b7,righttrigger:b8,dpup:h0.1,dpleft:h0.8,dpdown:h0.4,dpright:h0.2,"
```

## Related projects

- [joycond-cemuhook](https://github.com/joaorb64/joycond-cemuhook): Support for cemuhook's UDP protocol for gyroscope
- [DSU pad test](https://files.sshnuke.net/PadTest_1011.zip): cemuhook gyroscope test, works well under wine, screenshot [here](https://raw.githubusercontent.com/marcowindt/WiiMoteDSU/master/windows-pad-test.gif)
- [Antimicrox](https://github.com/AntiMicroX/antimicrox): tests buttons and provides SDL string
