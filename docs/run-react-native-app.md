---
created: 14.07.2021
tags: reactNative cli
---

# Start react native app in android emulator

```shell
npx react-native run-android
```

Known errors:
App already installed

```shell
npx react-native run-android
...
...
...
* What went wrong:
Execution failed for task ':app:installDebug'.
> java.util.concurrent.ExecutionException: com.android.builder.testing.api.DeviceException: com.android.ddmlib.InstallException: INSTALL_FAILED_VERSION_DOWNGRADE
```

[https://stackoverflow.com/a/13809076](https://stackoverflow.com/a/13809076)