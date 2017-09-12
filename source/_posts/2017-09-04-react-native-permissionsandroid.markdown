---
layout: post
title: "PermissionsAndroid 坑"
date: 2017-09-04 17:50:59 +0800
comments: true
categories: ReactNative
---
# Andoird 6.0 PermissionsAndroid 坑

## 前言

最近開發公司的RN專案遇到一個問題，明明在 `AndroidManifest.xml`有加入了
`
  <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
`
，但在執行的時候還是會噴error，接著就直接crash。
[![error-message](https://s26.postimg.org/tjoxllyft/21706759_1435564026520969_1452689658_o.png)](https://postimg.org/image/9cbhtb0yd/)

到應用程式的設定去看，會發現**位置**的授權並沒有被開啟，可是我記得在`Andoird 5.0`之前是沒有這個問題的，最近把開發機升級到`Andoird 7.0`才遇到。


## 正文

深入研究後，才發現在`Andoird 6.0 (API 23)` 之後，危險權限都需要動態取得使用者授權。貼心的是React Native 有提供 `PermissionsAndroid` 的 API 來供你使用👏👏

那 `PermissionsAndroid` 有提供三個 Methods:

### check (permission)
檢查權限
>Returns a promise resolving to a boolean value as to whether the specified permissions has been granted

範例：
```javascript
//檢查 Loaction Permission 為例

async checkLocationPermission() {
    try {
      const granted = await PermissionsAndroid.check(
        PermissionsAndroid.PERMISSIONS.ACCESS_FINE_LOCATION
      );
      if (granted === PermissionsAndroid.RESULTS.GRANTED) {
        console.log('客官已授予位置的權限');
      } else {
        console.log('客官尚未授予位置權限')
      }
    } catch (err) {
      console.warn(err);
    }
  }

```
### request(permission, rationale?)
請求權限
>Prompts the user to enable a permission and returns a promise resolving to a string value indicating whether the user allowed or denied the request

>If the optional rationale argument is included (which is an object with a title and message), this function checks with the OS whether it is necessary to show a dialog explaining why the permission is needed (https://developer.android.com/training/permissions/requesting.html#explain) and then shows the system permission dialog

rationale的參數可有可無，如果沒有的話，跳窗（dialog）就會顯示預設的訊息。

範例：
```javascript
//請求 Camera Permission 為例

async requestCameraPermission() {
  try {
    const granted = await PermissionsAndroid.request(
      PermissionsAndroid.PERMISSIONS.CAMERA,
      {
        'title': 'Cool Photo App Camera Permission',
        'message': 'Cool Photo App needs access to your camera ' +
                   'so you can take awesome pictures.'
      }
    )
    if (granted === PermissionsAndroid.RESULTS.GRANTED) {
      console.log("You can use the camera")
    } else {
      console.log("Camera permission denied")
    }
  } catch (err) {
    console.warn(err)
  }
}
```

### requestMultiple(permissions)
請求多個權限
>Prompts the user to enable multiple permissions in the same dialog and returns an object with the permissions as keys and strings as values indicating whether the user allowed or denied the request

### 使用流程
我的使用流程會先去check 使用者是否已授權此權限，如果沒有的話則向使用者發出請求。

範例：
```javascript

componentWillMount() {
  this.checkLocationPermission();
}


// 檢查使用者的位置授權
async checkLocationPermission() {
  try {
    const granted = await PermissionsAndroid.check(
      PermissionsAndroid.PERMISSIONS.ACCESS_FINE_LOCATION
    );
    if (granted === PermissionsAndroid.RESULTS.GRANTED || granted === true) {
      // 有拿到授權才去要 GPS
      this.askForGPS();
    } else {
      // 沒有授權的話就去向使用者請求
      this.requestLocationPermission();
    }
  } catch (err) {
    console.warn(err);
  }
}

async askForGPS() {
  //如果使用者沒有開啟GPS的話，要去跟他要
  LocationServicesDialogBox.checkLocationServicesIsEnabled({
      message: '<h2>Use Location ?</h2>This app wants to change your device settings:<br/><br/>Use GPS, Wi-Fi, and cell network for location<br/><br/>',
      ok: 'YES',
      cancel: 'NO'
  }).then((success) => {
      //如果使用者有開啟gps才去抓他的位置
      navigator.geolocation.getCurrentPosition(
        (position) => {
          console.log(position.coords.latitude);
          console.log(position.coords.longitude);
        },
        (error) => { console.log(error); },
        { enableHighAccuracy: false, timeout: 20000, maximumAge: 1000 },
      );
      console.log(success); // success => "enabled"
  }).catch((error) => {
      this.setState({ alertVisible: true });
      console.log(error.message); // error.message => "disabled"
  });
}

async requestLocationPermission() {
  try {
    const granted = await PermissionsAndroid.request(
      PermissionsAndroid.PERMISSIONS.ACCESS_FINE_LOCATION
    );
    if (granted === PermissionsAndroid.RESULTS.GRANTED  || granted === true) {
      console.log('現在你獲得GPS權限了');
      this.askForGPS();
    } else {
      console.log('用戶不理你');
    }
  } catch (err) {
    console.warn(err);
  }
}
```

這邊補充說明一下
```javascript
  if (granted === PermissionsAndroid.RESULTS.GRANTED  || granted === true){}
```
這邊要另外寫`granted === true` 是因為SDK 小於23 的話是回傳 true

> On devices before SDK version 23, the permissions are automatically granted if they appear in the manifest, so check and request should always be true.

### 叮嚀
在測試這塊的時候要記得，除了測 SDK >= 23的版本之外， SDK < 23 的也要記得測試。

## 參考資料
[https://facebook.github.io/react-native/docs/permissionsandroid.html](https://facebook.github.io/react-native/docs/permissionsandroid.html)
