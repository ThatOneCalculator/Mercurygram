[![Releases](https://img.shields.io/github/release/drizzt/Mercurygram.svg)](https://github.com/drizzt/Mercurygram/releases/latest)
[![Discussions](https://img.shields.io/badge/Official-Group-blue.svg?logo=telegram)](https://t.me/Mercurygram)

# Mercurygram

[Telegram](https://telegram.org) is a messaging app with a focus on speed and security. It’s superfast, simple and free.

This is an unofficial fork of the [FOSS-friendly fork](https://github.com/Telegram-FOSS-Team/Telegram-FOSS) of [Telegram App for Android](https://github.com/DrKLO/Telegram).

This includes the following additional features:

- Add ID in Profile Info
- Add a menu in Notifications and Sounds in order to set the UnifiedPush Distributors. The same menu may be longclicked in order to know if UnifiedPush notifications are working correctly.
- Add toggle setting in Chat Settings to start video messages with rear-facing camera
- Add toggle setting in Chat Settings to hide keyboard on chat scroll
- Add toggle setting in Chat Setting to hide "All Chats" tab (feature from NekoX)
- Add toggle setting in Debug Menu to enable Message Details menu
- Add toggle setting in Debug Menu to disable Unified Push support
- Add toggle setting in Debug Menu to disable Secure Flags. This option must **only** be used for debugging.
- Unlock premium app icons for anybody
- Large photos are sent (2560px instead of 1280px)
- Telegram application icons are replaced with [hermes wing (Created by Anthony Ledoux from Noun Project)](https://thenounproject.com/icon/hermes-wing-3559879/)

## NOTES

In order to have reliable notifications, it may be necessary to set battery
optimization to Not optimized for Mercurygram (no, it won't use more battery).

Background Connections setting is not necessary and uses lot of battery, so
please disable it when you use UnifiedPush.

If you set Battery optimization to Not optimized, Keep-Alive Service will be not
necessary.

See [dontkillmyapp](https://dontkillmyapp.com/) for more information.

If you can't/want set Battery optimization to Not optimized and you don't
receive notifications after a while (more than 30 minutes) please enable
Keep-Alive Service instead.

## Why the name Mercurygram?

For a couple of reasons:

- Mercury is the Roman, and I'm Italian, God and the "**messenger** of the gods"
- The logo is a stylized 'F' representing his winged shoes, but it also resembles an 'F' in honor of **Freddy Mercury**.

## Current Maintainers

- [drizzt](https://github.com/drizzt)
- you? :)

## Contributors
- [quqkuk](https://github.com/quqkuk)

## Current Telegram-FOSS Maintainers

- [thermatk](https://github.com/thermatk)
- you? :)

## Telegram-FOSS Contributors

- [slp](https://github.com/slp)
- [Bubu](https://github.com/Bubu)
- [Sudokamikaze](https://github.com/Sudokamikaze)
- [l2dy](https://github.com/l2dy)
- [maximgrafin](https://github.com/maximgrafin)
- [vn971](https://github.com/vn971)
- [theel0ja](https://github.com/theel0ja)
- [AnXh3L0](https://github.com/AnXh3L0)
- [noplanman](https://github.com/noplanman)
- [vk496](https://github.com/vk496)
- [verdulo](https://github.com/verdulo)
- [anupritaisno1](https://github.com/anupritaisno1)
- [nekohasekai](https://github.com/nekohasekai)
- [kdrag0n](https://github.com/kdrag0n)
- [terachad](https://github.com/terachad)
- [ppnplus](https://github.com/ppnplus)
- [luvletter2333](https://github.com/luvletter2333)
- [23rd](https://github.com/23rd)
- [proletarius101](https://github.com/proletarius101)
- [CWJamieson](https://github.com/CWJamieson)
- [verdulo](https://github.com/verdulo)
- [tehcneko](https://github.com/tehcneko)

## Changes:

*Replacement of non-FOSS, untrustworthy or suspicious binaries or source code:*
- Do location sharing with OpenStreetMap(osmdroid) instead of Google Maps
- Use Noto emoji set instead of Apple's emoji
- Google Play Services GCM replaced with [UnifiedPush](https://unifiedpush.org)
- **SECURITY:** BoringSSL prebuilts are replaced with recent upstream source code built at compile time
- **SECURITY:** FFmpeg prebuilts are replaced with recent upstream source code built at compile time
- **SECURITY:** libvpx prebuilts are replaced with recent upstream source code built at compile time
- **SECURITY:** Bundled libWebP is updated

*Removal of non-FOSS, untrustworthy or suspicious binaries or source code and their functionality:*
- Google Vision face detection and barcode scanning (Passport)
- Google Wallet and Android Pay integration
- Google Voice integration
- HockeyApp crash reporting and self-updates
- Google SMS retrieval
- Google ML Kit

*Other:*
- Added the ability to parse locations from intents containing a `geo:<lat>,<lon>,<zoom>` string
- Force static map previews from Telegram
- No content restrictions

## Versioning

This repository contains tags to make tracking versions easier.

Versions are in form "$UPSTREAM.$RELEASE" where:

* $UPSTREAM is the tag of Telegram-FOSS upstream.
* $RELEASE is a number ([0-9]\*), indicating minor releases between official Telegram-FOSS versions.

## API, Protocol documentation

Telegram API manuals: https://core.telegram.org/api

MTproto protocol manuals: https://core.telegram.org/mtproto

## Building

**NOTE: Building on Windows is, unfortunately, not supported.
Consider using a Linux VM or dual booting.**
![WindowsSupport](/tgfoss-build-under-win.gif?raw=true)

**Important:**

1. You need the Android NDK, Go(Golang) and [Ninja](https://ninja-build.org/) to build the apk.

2. Don't forget to include the submodules when you clone:
      - `git clone --recursive https://github.com/drizzt/Mercurygram.git`

3. Build native FFmpeg and BoringSSL dependencies:
      - Go to the `TMessagesProj/jni` folder and execute the following (define the paths to your NDK and Ninja):

      ```
      export NDK=[PATH_TO_NDK]
      export NINJA_PATH=[PATH_TO_NINJA]
      ./build_libvpx_clang.sh
      ./build_ffmpeg_clang.sh
      ./patch_ffmpeg.sh
      ./patch_boringssl.sh
      ./build_boringssl.sh
      ```

4. If you want to publish a modified version of Telegram:
      - You should get **your own API key** here: https://core.telegram.org/api/obtaining\_api\_id and create a file called `API_KEYS` in the source root directory.
        The contents should look like this:
        ```
        APP_ID = 12345
        APP_HASH = aaaaaaaabbbbbbccccccfffffff001122
        ```
      - Do not use the name Telegram and the standard logo (white paper plane in a blue circle) for your app — or make sure your users understand that it is unofficial
      - Take good care of your users' data and privacy
      - **Please remember to publish your code too in order to comply with the licenses**

The project can be built with Android Studio or from the command line with gradle:

`./gradlew assembleAfatRelease`

# DIGITAL RESISTANCE

![DIGITALRESISTANCE](/DigitalResistance.jpg?raw=true "DIGITALRESISTANCE")
