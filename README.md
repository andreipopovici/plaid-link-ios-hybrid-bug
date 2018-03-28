# Plaid Link bug in iOS hybrid apps

# UPDATE (3/28/18)

It looks like this was caused by a change in Cordova's whitelist plugin. The fix is to add

```<allow-navigation href="*" />```

inside `<widget>` in `config.xml`. Of course, the URL could then be refined to only allow Plaid's CDN for Link files.

Please see https://github.com/plaid/link/issues/237 for more details.

## Contents:

- Vue.js webapp created using Quasar Framework v.14 CLI tool
- integrates with Cordova using `quasar wrap cordova`
- relevant code sample is in [`src/components/Hello.vue`](https://github.com/andreipopovici/plaid-link-ios-hybrid-bug/blob/master/src/components/Hello.vue)

## Steps to reproduce:

1. Load webapp using `quasar dev`, `onLoad` handler gets called.
2. Run hybrid app in Android emulator, `onLoad` handler gets called.
3. Run hybrid app in iOS emulator, `onLoad` handler **DOES NOT** get called.

## Setup Steps:

``` bash
# install dependencies
$ npm install

# export env var
$ export PLAID_PUBLIC_KEY='<your key here>'

# serve with hot reload at localhost:8080
$ quasar dev

# build for production with minification
$ quasar build

# add relevant mobile platforms using cordova
$ cd cordova
$ cordova platform add android ios
$ cordova requirements

# Manually fix recent Android build issue by following:
# [Temporary solution to Android build bug](https://github.com/crosswalk-project/cordova-plugin-crosswalk-webview/issues/205#issuecomment-372283362)

# Run emulators
$ cordova emulate android
$ cordova emulate ios
```
