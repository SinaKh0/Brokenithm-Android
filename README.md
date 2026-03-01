## Brokenithm-Slide-Android

A fork of [Brokenithm-Android](https://github.com/tindy2013/Brokenithm-Android) that removes the air sensor input, leaving only the touch slider.

Air sensor input has been removed. This app is intended to be used alongside [Brokenithm-Hands-Android](https://github.com/SinaKh0/Brokenithm-Hands-Android) handling air input, with two instances of the [modified server](https://github.com/SinaKh0/Brokenithm-Android-Server) using the `-s` (slider only) and `-a` (air only) flags to split input across two devices.

Supports UDP and TCP connection to host. TCP recommended for lower latency.

<p align="center">
  <img src="screenshots/Screenshot.jpg" width="500" alt="screenshot"/>
</p>

## Slider Zones

The original Brokenithm-Android slider uses 16 touch zones. This app uses all 32 zones directly across the full screen width, matching the physical arcade slider hardware which has 32 individual capacitive sensors side by side.

An alternative **Brokenithm-iOS-style mode** is available in settings which splits the screen into 16 horizontal zones, each divided into a top and bottom half for 32 total inputs, matching the behavior of Brokenithm-iOS.

In settings: **Horizontal 32 Zones** - when enabled (default), the full screen width is divided into 32 equal zones mapped directly to the 32 game inputs. When disabled, switches to Brokenithm-iOS-style mode: 16 horizontal zones each split into top/bottom half.


## Dual Device Setup

To use both apps together, run two server instances on Windows:
```bash
brokenithm.exe -T -s -p 52468  # slider instance
brokenithm.exe -T -a -p 52469  # air instance
```

Connect this app to port 52468 and Brokenithm-Hands-Android on the other android device to port 52469.

## Low Latency Setup (USB)

For the lowest latency, connect your devices via USB and use ADB reverse port forwarding instead of WiFi. With both devices plugged in run:
```bash
adb devices  # to get serial of both devices
adb -s <slider_device_serial> reverse tcp:52468 tcp:52468
adb -s <hands_device_serial> reverse tcp:52469 tcp:52469
```

Then in each app use `127.0.0.1:PORT` as the server address and enable TCP mode.