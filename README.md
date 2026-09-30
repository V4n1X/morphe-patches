# 🍃 V4n1X Patches

Patches for use with [Morphe](https://morphe.software).

## ❓ About

A collection of bytecode/resource patches for Android apps, built for the Morphe patcher.
Supports SoundCloud (`com.soundcloud.android`) and Parcello (`org.parcello`).

## 📚 How to use

Click here to add these patches to Morphe:

> https://morphe.software/add-source?github=V4n1X/morphe-patches

Or manually add this repository URL in Morphe Manager → Sources:

> `https://github.com/V4n1X/morphe-patches`

## 📦 Parcello: Disable ads

**Supported APK:** Parcello **2.2.20**, package `org.parcello`, version code `200220`, Android 8.0+.
Support is **experimental** until an on-device smoke test has been completed.

The default **Disable ads** patch:

- Disables AdMob initialization, banner/interstitial/rewarded ads, and advertising consent dialogs.
- Removes the automatic Mobile Ads initialization provider, ad-only Android components and advertising permissions.
- Removes the Symplr/advertising consent bootstrap, preventing its Outbrain loading path.
- Hides ad slots and promotional banners and neutralizes direct sponsor image downloads and links.
- Preserves delayed push-notification initialization, tracking data, barcode scanning, and purchase entitlements.

This disables advertising; it does **not** delete every bundled SDK class, unlock premium, or disable all analytics.
The supplied APK has passed local Morphe patch execution, resource/DEX compilation and JavaScript checks;
actual app startup, tracking, login, scanning and notifications still need testing on an Android device.

### Using the new patch

For local testing, import the built `.mpp` bundle from `patches/build/libs/` in Morphe Manager,
select the original Parcello 2.2.20 APK and enable **Disable ads**. Experimental targets may need
to be shown/enabled in the Manager. Do not use a previously modified APK.

For distribution through the existing GitHub source, commit the feature with a conventional message
such as `feat(parcello): disable advertising in version 2.2.20`, then publish it to `main`.
The existing Release workflow builds the bundle and updates the patch list, README and source metadata.
**Until that release is published, the existing GitHub source still serves the old bundle.**
Original/decompiled/patched APK files must remain local and must not be included in a commit or release.

## ⚖️ Disclaimer

This project is provided for **educational purposes only**. The patches are intended to help developers
understand Android bytecode modification and the Morphe patching framework.

- **No affiliation** — This project is not affiliated with, endorsed by, or connected to any of the patched applications or their developers.
- **No warranty** — These patches are provided "as is" without warranty of any kind. Use at your own risk.
- **Terms of Service** — Using modified versions of applications may violate their Terms of Service. It is your responsibility to review and comply with applicable terms.
- **No redistribution** — The patched APK files should not be redistributed. These patches are meant to be applied by end users to their own legally obtained APKs.
- **Fair use** — These patches are developed through independent reverse engineering for interoperability and personal use, consistent with fair use principles.

The author assumes no liability for any consequences resulting from the use of these patches.

## 🙏 Credits

Based on patches from:

- [hoo-dles/morphe-patches](https://github.com/hoo-dles/morphe-patches) — AMOLED dark theme, analytics/telemetry patch
- [kondratjev/morphe-patches](https://github.com/kondratjev/morphe-patches) — Enable SoundCloud Go, consent popup & analytics patches

Built on the official [MorpheApp/morphe-patches-template](https://github.com/MorpheApp/morphe-patches-template).

<!-- PATCHES_START EXPANDED -->
> **Local source:** `main` • 6 patches total. Latest published release: [v1.3.0](https://github.com/V4n1X/morphe-patches/releases/tag/v1.3.0) (without Parcello).
<details open>
<summary>📦 SoundCloud&nbsp;&nbsp;•&nbsp;&nbsp;5 patches</summary>
<br>

**🎯 Supported versions:**

| 2026.08.26-release |
| :---: |

| 💊&nbsp;Patch | 📜&nbsp;Description | ⚙️&nbsp;Options |
|----------|----------------|-----------|
| [AMOLED dark theme](#amoled-dark-theme) | Changes the default dark theme to use true blacks for AMOLED screens. |  |
| [Disable analytics](#disable-analytics) | Disables SoundCloud's analytics. |  |
| [Disable consent popup](#disable-consent-popup) | Disables the OneTrust consent/cookies popup and collapses banner views. |  |
| [Enable SoundCloud Go+](#enable-soundcloud-go) | Enables SoundCloud Go+ premium features, offline listening, HQ audio, and disables audio/visual ads. |  |
| [Material You dynamic theme](#material-you-dynamic-theme) | Applies Android 12+ Material You dynamic accent colors from the system wallpaper palette. |  |

</details>

<details open>
<summary>📦 Parcello&nbsp;&nbsp;•&nbsp;&nbsp;1 patch</summary>
<br>

**🎯 Supported versions:**

| 🧪&nbsp;2.2.20 |
| :---: |

| 💊&nbsp;Patch | 📜&nbsp;Description | ⚙️&nbsp;Options |
|----------|----------------|-----------|
| [Disable ads](#parcello-disable-ads) | Disables AdMob ads and advertising consent prompts; removes sponsored/promotional banners. |  |

</details>

<!-- PATCHES_END -->

## 🛠️ Building

```sh
./gradlew buildAndroid
```

The built `.mpp` file will be at `patches/build/libs/`.
Use **JDK 21**, as in CI. The Morphe dependency registry requires `gpr.user` / `gpr.key`
Gradle properties or the `GITHUB_ACTOR` / `GITHUB_TOKEN` environment variables.
Never commit access tokens.

### Verification

```sh
# Builds the Android bundle and runs resource regression checks (no APK needed).
./gradlew :patches:buildAndroid :patches:check

# Also applies the patch to a legally obtained original APK and rebuilds it locally.
./gradlew :patches:buildAndroid :patches:testParcelloAds \
  -PparcelloApk='APK/Parcello+Sendungsverfolgung+-+_2.2.20_APKPure.apk'
```

The optional APK test verifies bundle discovery, native AdMob method bodies and modified assets.
When Node.js is available, it also syntax-checks the JavaScript and tests advertising promises
and delayed notification setup without network requests. Test artifacts stay in the ignored build directory.
`./gradlew :patches:generatePatchesList` regenerates metadata from the current bundle, not older build artifacts.

## 📜 License

V4n1X Patches are licensed under the [GNU General Public License v3.0](LICENSE)
