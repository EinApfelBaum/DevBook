---
created: 14.07.2021
tags: android cli cheatSheet
parent: Cheat sheets
---

# Android debug bridge (adb)

```bash
# list all connected devices
adb devices

# list all reverse
adb reverse --list

# set revers for specific device
# https://blog.usejournal.com/adb-port-forwarding-and-reversing-d2bc71835d43
adb -s emulator-5554 reverse tcp:3000 tcp:3000

# show logs
adb -s emulator-5554  logcat *:S ReactNative:V ReactNativeJS:V

# install apk
adb -s emulator-5554 install myapp.apk
```
