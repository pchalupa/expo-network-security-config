# Expo Network Security Config

This [Expo config plugin](https://docs.expo.dev/config-plugins/introduction/) allows you to include a [network security config](https://developer.android.com/privacy-and-security/security-config) within your app.
This is helpful in cases when you need to allow HTTPS interception for tools like [Proxyman](https://developer.android.com/privacy-and-security/security-config) in your Android app.

### Platform Compatibility

| Android Device | Android Emulator | iOS Device | iOS Simulator | Web |
| -------------- | ---------------- | ---------- | ------------- | --- |
| ✅             | ✅               | ❌         | ❌            | ❌  |

## Usage

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

| Parameter             | Description                         |
| --------------------- | ----------------------------------- |
| networkSecurityConfig | Path to network_security_config.xml |
| enable                | Enable or disable this config       |
