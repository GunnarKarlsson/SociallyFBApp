# Socially (free / ads)

This is the **free, ad-supported Android app** for **Socially**, a third-party Facebook client. Socially let users restyle the app with interchangeable skins and themes (backgrounds, action bar colors, sliding-menu colors, fonts, and a custom color picker) instead of using Facebook’s default look.

It was a separate Google Play listing from the paid, ads-free build. The client itself lives in the sibling **socially_base_lib** project; this repo is the application wrapper that turns that library into the free store app and supplies the skin pack.

Package: `com.bluebitapps.fbclient`  
Type: Eclipse ADT / Ant Android application  
Min SDK: 14 · Target SDK: 17  
Store version: `1.00053` (`versionCode` 53)

Live on Google Play **2012–2014**.

## How this project relates to the library

`socially_base_lib` (`com.bluebitapps.fbclientbase`) holds Graph API access, the navigation shell, theming engine, and all feature screens (news feed, photos, chat, notifications, events, groups, and so on). See that project’s README for the full feature list.

This app:

- Depends on `socially_base_lib` as an Android library (`android.library.reference.2=../socially_base_lib`)
- Sets `isPremiumVersion` to **false**, which shows AdMob banners and a “Remove ads” item that opens the paid listing (`com.bluebitapps.sociallypremium`)
- Declares Google Play Ads (`com.google.android.gms.ads.AdActivity`) and in-app billing
- Provides the Facebook app id and about 160 built-in skins
- Has **no Java sources of its own** — `FBClientApplication`, `LaunchActivity`, and the rest come from the library

A paid counterpart existed as a separate application project with `isPremiumVersion` true (no banners). Socially Pink was another store variant (`com.bluebitapps.sociallypinkpremium` for its paid listing).

## What this app adds

### Ads and billing

- `res/values/config_version.xml` — Facebook app id `395995423749684` and `isPremiumVersion=false`
- AdMob banners on library screens that include an `AdView` (loaded from `BaseFragment` when the premium flag is off)
- `BILLING` permission for Google Play in-app billing
- Settings / sliding-menu “Remove ads” deep-link to the paid Socially package

### Skins and themes

Themes are declared in `res/xml/app_themes.xml` and applied by the library’s `ThemeFactory`. This app ships the drawable backgrounds, preview icons, and action-bar / menu colors for the store build (named skins such as Blue, Pink, Purple Rain, Black Leather, plus numbered theme packs).

### Fonts

Bundled typefaces in `assets/fonts/`: Arial, Roboto, Verdana, Garamond, Gill, BM Solid, Cute. The library uses these for the in-app text-appearance settings.

### Preferences overlay

`res/xml/preferences.xml` overlays notification delivery, news-feed refresh, and text appearance settings on top of the library defaults.

## Project layout

```
AndroidManifest.xml     Application id, ads activity, billing, library activities/services
res/xml/app_themes.xml  Skin catalog
res/values/             App id, premium flag, theme colors
res/drawable*/          Theme backgrounds and icons
res/xml/preferences.xml Settings overlay
assets/fonts/           Bundled typefaces
libs/                   android-support-v4.jar
```

External Eclipse library references (not all in this repo): `socially_base_lib`, Facebook Android SDK, Google Play services.

## License

MIT. See [LICENSE](LICENSE).
