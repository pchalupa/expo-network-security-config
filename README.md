# Expo Network Security Config

This [Expo config plugin](https://docs.expo.dev/config-plugins/introduction/) allows you to include a [network security config](https://developer.android.com/privacy-and-security/security-config) within your app.
This is helpful in cases when you need to allow HTTPS interception for tools like [Proxyman](https://developer.android.com/privacy-and-security/security-config) in your Android app.

### Platform Compatibility

| Android Device | Android Emulator | iOS Device | iOS Simulator | Web |
| -------------- | ---------------- | ---------- | ------------- | --- |
| ✅             | ✅               | ❌         | ❌            | ❌  |

## Usage

```js
{
  plugins: [
    [
      'expo-network-security-config',
      {
        networkSecurityConfig: './assets/configs/network_security_config.xml',
        enable: true,
      },
    ],
  ];
}
```

## API

| Parameter             | Description                         |
| --------------------- | ----------------------------------- |
| networkSecurityConfig | Path to network_security_config.xml |
| enable                | Enable or disable this config       |
