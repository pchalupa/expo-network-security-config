# Expo Network Security Config

An [Expo config plugin](https://docs.expo.dev/config-plugins/introduction/) that copies a custom [network security config](https://developer.android.com/privacy-and-security/security-config) into your Android app.
This is useful when you need to allow HTTPS interception for tools like [Proxyman](https://proxyman.io/) on Android.

### Platform Compatibility

| Android Device | Android Emulator | iOS Device | iOS Simulator | Web |
| -------------- | ---------------- | ---------- | ------------- | --- |
| ✅             | ✅               | ❌         | ❌            | ❌  |

## Installation

```sh
npx expo install expo-network-security-config
```

Requires **Expo SDK 50+**.

## Usage

1. Create your `network_security_config.xml` file somewhere in your project (e.g. `assets/configs/network_security_config.xml`).

2. Add the plugin to the `plugins` array in your `app.json` (or `app.config.js`):

```json
{
  "plugins": [
    [
      "expo-network-security-config",
      {
        "networkSecurityConfig": "./assets/configs/network_security_config.xml",
        "enable": true
      }
    ]
  ]
}
```

3. Run prebuild to regenerate the native project:

```sh
npx expo prebuild
```

The plugin copies your XML file into `android/app/src/main/res/xml/` and adds `android:networkSecurityConfig` to `AndroidManifest.xml`.

### Example Config

The following example allows [Proxyman](https://proxyman.io/) to intercept HTTP/HTTPS requests by trusting user-added CAs:

```xml
<network-security-config>
  <debug-overrides>
    <trust-anchors>
      <!-- Trust user added CAs while debuggable only -->
      <certificates src="user" />
      <certificates src="system" />
    </trust-anchors>
  </debug-overrides>

  <base-config cleartextTrafficPermitted="true">
    <trust-anchors>
      <certificates src="system" />
      <certificates src="user" />
    </trust-anchors>
  </base-config>
</network-security-config>
```

## API

| Parameter               | Description                                                                                      |
| ----------------------- | ------------------------------------------------------------------------------------------------ |
| `networkSecurityConfig` | Path to your `network_security_config.xml` file, relative to the project root.                   |
| `enable`                | When `true`, the config is copied and applied. When `false` (or omitted), the plugin is skipped. |
