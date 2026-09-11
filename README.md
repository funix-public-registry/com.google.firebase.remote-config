# com.google.firebase.remote-config

## Requirements

- Unity 2021.3 or newer
- Internet access at Android/iOS build time (see below)
- For iOS builds: CocoaPods installed on the build machine

## Installation

Add the following to your project's `Packages/manifest.json` under `"dependencies"`:

```json
"com.google.external-dependency-manager": "https://github.com/funix-public-registry/com.google.external-dependency-manager.git#1.2.186",
"com.google.firebase.app": "https://github.com/funix-public-registry/com.google.firebase.app.git#13.16.0",
"com.google.firebase.remote-config": "https://github.com/funix-public-registry/com.google.firebase.remote-config.git#13.16.0"
```

`com.google.external-dependency-manager` (EDM4U) is required — it resolves the
real native libraries at build time (see "How this works" below).

Pin the version tag (`#v13.16.0`) to the release you want. Always match this version across every `com.google.firebase.*`
package you install in the same project.

## Firebase Console setup

You must configure this app in the [Firebase Console](https://console.firebase.google.com)
and add the resulting config file to your project:
- Android: `google-services.json` → project root
- iOS: `GoogleService-Info.plist` → project root

Without this, Firebase will fail to initialize at runtime.

## How this works

- **Android**: this package ships small `Dependencies.xml` declarations, not the
  compiled `.aar` files themselves. EDM4U's Android Resolver downloads the real
  libraries from Google's Maven repository automatically when you switch platform
  or build for Android — this requires network access on the build machine.
- **iOS**: EDM4U's iOS Resolver runs CocoaPods (`pod install`) during Xcode
  project generation to pull in the real frameworks — the build machine needs
  CocoaPods installed and network access.

Neither of these steps requires manual action; both trigger automatically as
part of a normal Android/iOS build.

## Troubleshooting

- **`DllNotFoundException` / `ClassNotFoundException` at runtime on Android**:
  usually means Android Resolver hasn't run — try `Assets > External Dependency
  Manager > Android Resolver > Resolve`.
- **iOS build fails at `pod install`**: confirm CocoaPods is installed on the
  build machine (`sudo gem install cocoapods`).

## License

This is a redistribution wrapper around Google's official Firebase Unity SDK,
governed by [Firebase's Terms of Service](https://firebase.google.com/terms)
and the [Firebase Unity SDK release notes](https://firebase.google.com/support/release-notes/unity).