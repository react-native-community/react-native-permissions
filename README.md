# ☝🏼 React Native Permissions

[![npm version](https://badge.fury.io/js/react-native-permissions.svg)](https://badge.fury.io/js/react-native-permissions)
[![npm](https://img.shields.io/npm/dt/react-native-permissions.svg)](https://www.npmjs.org/package/react-native-permissions)
![Platform - Android, iOS and Windows](https://img.shields.io/badge/platform-Android%20%7C%20iOS%20%7C%20Windows-yellow.svg)
![MIT](https://img.shields.io/dub/l/vibe-d.svg)
[![styled with prettier](https://img.shields.io/badge/styled_with-prettier-ff69b4.svg)](https://github.com/prettier/prettier)

A unified permissions API for React Native on iOS, Android and Windows.

For Windows only builds 18362 and later are supported.

**👉 Try and give feedbacks about [the next major version (3.0.0)](https://github.com/zoontek/react-native-permissions/tree/3.0.0)!**

## Support

| version | react-native version |
| ------- | -------------------- |
| 2.0.0+  | 0.60.2+              |

## Setup

```bash
$ npm install --save react-native-permissions
# --- or ---
$ yarn add react-native-permissions
```

### iOS

By default no permission handler is installed. Update your `Podfile` by choosing the ones you want to check or request, then run `pod install`.

```ruby
target 'YourAwesomeProject' do

  # …

  permissions_path = '../node_modules/react-native-permissions/ios'

  pod 'Permission-AppTrackingTransparency', :path => "#{permissions_path}/AppTrackingTransparency.podspec"
  pod 'Permission-BluetoothPeripheral', :path => "#{permissions_path}/BluetoothPeripheral.podspec"
  pod 'Permission-Calendars', :path => "#{permissions_path}/Calendars.podspec"
  pod 'Permission-Camera', :path => "#{permissions_path}/Camera.podspec"
  pod 'Permission-Contacts', :path => "#{permissions_path}/Contacts.podspec"
  pod 'Permission-FaceID', :path => "#{permissions_path}/FaceID.podspec"
  pod 'Permission-LocationAlways', :path => "#{permissions_path}/LocationAlways.podspec"
  pod 'Permission-LocationWhenInUse', :path => "#{permissions_path}/LocationWhenInUse.podspec"
  pod 'Permission-MediaLibrary', :path => "#{permissions_path}/MediaLibrary.podspec"
  pod 'Permission-Microphone', :path => "#{permissions_path}/Microphone.podspec"
  pod 'Permission-Motion', :path => "#{permissions_path}/Motion.podspec"
  pod 'Permission-Notifications', :path => "#{permissions_path}/Notifications.podspec"
  pod 'Permission-PhotoLibrary', :path => "#{permissions_path}/PhotoLibrary.podspec"
  pod 'Permission-Reminders', :path => "#{permissions_path}/Reminders.podspec"
  pod 'Permission-Siri', :path => "#{permissions_path}/Siri.podspec"
  pod 'Permission-SpeechRecognition', :path => "#{permissions_path}/SpeechRecognition.podspec"
  pod 'Permission-StoreKit', :path => "#{permissions_path}/StoreKit.podspec"

end
```

> :warning: If you see a **No permission handler detected** error: Make sure that you have at least one permission handler set up. In some cases the Xcode cache needs to be cleared (`Xcode -> Product -> Clean Build Folder`)

Then update your `Info.plist` with wanted permissions usage descriptions:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>

  <!-- 🚨 Keep only the permissions used in your app 🚨 -->

  <key>NSAppleMusicUsageDescription</key>
  <string>YOUR TEXT</string>
  <key>NSBluetoothAlwaysUsageDescription</key>
  <string>YOUR TEXT</string>
  <key>NSBluetoothPeripheralUsageDescription</key>
  <string>YOUR TEXT</string>
  <key>NSCalendarsUsageDescription</key>
  <string>YOUR TEXT</string>
  <key>NSCameraUsageDescription</key>
  <string>YOUR TEXT</string>
  <key>NSContactsUsageDescription</key>
  <string>YOUR TEXT</string>
  <key>NSFaceIDUsageDescription</key>
  <string>YOUR TEXT</string>
  <key>NSLocationAlwaysAndWhenInUseUsageDescription</key>
  <string>YOUR TEXT</string>
  <key>NSLocationAlwaysUsageDescription</key>
  <string>YOUR TEXT</string>
  <key>NSLocationWhenInUseUsageDescription</key>
  <string>YOUR TEXT</string>
  <key>NSMicrophoneUsageDescription</key>
  <string>YOUR TEXT</string>
  <key>NSMotionUsageDescription</key>
  <string>YOUR TEXT</string>
  <key>NSPhotoLibraryUsageDescription</key>
  <string>YOUR TEXT</string>
  <key>NSRemindersUsageDescription</key>
  <string>YOUR TEXT</string>
  <key>NSSpeechRecognitionUsageDescription</key>
  <string>YOUR TEXT</string>
  <key>NSSiriUsageDescription</key>
  <string>YOUR TEXT</string>
  <key>NSUserTrackingUsageDescription</key>
  <string>YOUR TEXT</string>

  <!-- … -->

</dict>
</plist>
```

#### Workaround for `use_frameworks!` issues

If you use `use_frameworks!`, add this at the top of your `Podfile`:

```ruby
use_frameworks!

# Convert all permission pods into static libraries
pre_install do |installer|
  installer.pod_targets.each do |pod|
    if pod.name.eql?('RNPermissions') || pod.name.start_with?('Permission-')
      def pod.build_type;
        # Uncomment one line depending on your CocoaPods version
        # Pod::BuildType.static_library # >= 1.9
        # Pod::Target::BuildType.static_library # < 1.9
      end
    end
  end
end
```

### Android

Add all wanted permissions to your app `android/app/src/main/AndroidManifest.xml` file:

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
  package="com.myawesomeapp">

  <!-- 🚨 Keep only the permissions used in your app 🚨 -->

  <uses-permission android:name="android.permission.ACCEPT_HANDOVER" />
  <uses-permission android:name="android.permission.ACCESS_BACKGROUND_LOCATION" />
  <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
  <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
  <uses-permission android:name="android.permission.ACTIVITY_RECOGNITION" />
  <uses-permission android:name="android.permission.ANSWER_PHONE_CALLS" />
  <uses-permission android:name="android.permission.BODY_SENSORS" />
  <uses-permission android:name="android.permission.CALL_PHONE" />
  <uses-permission android:name="android.permission.CAMERA" />
  <uses-permission android:name="android.permission.GET_ACCOUNTS" />
  <uses-permission android:name="android.permission.PROCESS_OUTGOING_CALLS" />
  <uses-permission android:name="android.permission.READ_CALENDAR" />
  <uses-permission android:name="android.permission.READ_CALL_LOG" />
  <uses-permission android:name="android.permission.READ_CONTACTS" />
  <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
  <uses-permission android:name="android.permission.READ_PHONE_NUMBERS" />
  <uses-permission android:name="android.permission.READ_PHONE_STATE" />
  <uses-permission android:name="android.permission.READ_SMS" />
  <uses-permission android:name="android.permission.RECEIVE_MMS" />
  <uses-permission android:name="android.permission.RECEIVE_SMS" />
  <uses-permission android:name="android.permission.RECEIVE_WAP_PUSH" />
  <uses-permission android:name="android.permission.RECORD_AUDIO" />
  <uses-permission android:name="android.permission.SEND_SMS" />
  <uses-permission android:name="android.permission.USE_SIP" />
  <uses-permission android:name="android.permission.WRITE_CALENDAR" />
  <uses-permission android:name="android.permission.WRITE_CALL_LOG" />
  <uses-permission android:name="android.permission.WRITE_CONTACTS" />
  <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
  <uses-permission android:name="com.android.voicemail.permission.ADD_VOICEMAIL" />

  <!-- … -->

</manifest>
```

### Windows

Open the project solution file from the `windows` folder. In the app project open `Package.appxmanifest` file. From there you can select which capabilites you want your app to support.

## 🆘 Manual linking

Because this package targets React Native 0.60.0+, you probably won't need to link it manually. Otherwise if it's not the case, follow these additional instructions. You also need to manual link the module on Windows when using React Native Windows prior to 0.63:

<details>
  <summary><b>👀 See manual linking instructions</b></summary>

### iOS

Add this line to your `ios/Podfile` file, then run `pod install`.

```bash
target 'YourAwesomeProject' do
  # …
  pod 'RNPermissions', :path => '../node_modules/react-native-permissions'
end
```

### Android

1. Add the following lines to `android/settings.gradle`:

```gradle
include ':react-native-permissions'
project(':react-native-permissions').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-permissions/android')
```

2. Add the implementation line to the dependencies in `android/app/build.gradle`:

```gradle
dependencies {
  // ...
  implementation project(':react-native-permissions')
}
```

3. Add the import and link the package in `MainApplication.java`:

```java
import com.reactnativecommunity.rnpermissions.RNPermissionsPackage; // <- add the RNPermissionsPackage import

public class MainApplication extends Application implements ReactApplication {

  // …

  @Override
  protected List<ReactPackage> getPackages() {
    @SuppressWarnings("UnnecessaryLocalVariable")
    List<ReactPackage> packages = new PackageList(this).getPackages();
    // …
    packages.add(new RNPermissionsPackage());
    return packages;
  }

  // …
}
```

### Windows

1. In `windows/myapp.sln` add the `RNCConfig` project to your solution:

   - Open the solution in Visual Studio 2019
   - Right-click Solution icon in Solution Explorer > Add > Existing Project
   - Select `node_modules\react-native-permissions\windows\RNPermissions\RNPermissions.vcxproj`

2. In `windows/myapp/myapp.vcxproj` ad a reference to `RNPermissions` to your main application project. From Visual Studio 2019:

   - Right-click main application project > Add > Reference...
   - Check `RNPermissions` from Solution Projects.

3. In `pch.h` add `#include "winrt/RNPermissions.h"`.

4. In `app.cpp` add `PackageProviders().Append(winrt::RNPermissions::ReactPackageProvider());` before `InitializeComponent();`.

</details>

## Understanding permission flow

As permissions are not handled in the same way on iOS and Android, this library provides an abstraction over the two platforms' behaviors. To understand it a little better, take a look to these two flowcharts:

### iOS flow

```
   ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
   ┃ check(PERMISSIONS.IOS.CAMERA) ┃
   ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
                   │
       Is the feature available
           on this device ?
                   │           ╔════╗
                   ├───────────║ NO ║──────────────┐
                   │           ╚════╝              │
                ╔═════╗                            ▼
                ║ YES ║                 ┌─────────────────────┐
                ╚═════╝                 │ RESULTS.UNAVAILABLE │
                   │                    └─────────────────────┘
           Is the permission
             requestable ?
                   │           ╔════╗
                   ├───────────║ NO ║──────────────┐
                   │           ╚════╝              │
                ╔═════╗                            ▼
                ║ YES ║                  ┌───────────────────┐
                ╚═════╝                  │ RESULTS.BLOCKED / │
                   │                     │  RESULTS.GRANTED  │
                   ▼                     └───────────────────┘
          ┌────────────────┐
          │ RESULTS.DENIED │
          └────────────────┘
                   │
                   ▼
  ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
  ┃ request(PERMISSIONS.IOS.CAMERA) ┃
  ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
                   │
         Does the user accept
            the request ?
                   │           ╔════╗
                   ├───────────║ NO ║──────────────┐
                   │           ╚════╝              │
                ╔═════╗                            ▼
                ║ YES ║                   ┌─────────────────┐
                ╚═════╝                   │ RESULTS.BLOCKED │
                   │                      └─────────────────┘
                   ▼
          ┌─────────────────┐
          │ RESULTS.GRANTED │
          └─────────────────┘
```

### Android flow

```
 ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
 ┃ check(PERMISSIONS.ANDROID.CAMERA) ┃
 ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
                   │
       Is the feature available
           on this device ?
                   │           ╔════╗
                   ├───────────║ NO ║──────────────┐
                   │           ╚════╝              │
                ╔═════╗                            ▼
                ║ YES ║                 ┌─────────────────────┐
                ╚═════╝                 │ RESULTS.UNAVAILABLE │
                   │                    └─────────────────────┘
           Is the permission
             requestable ?
                   │           ╔════╗
                   ├───────────║ NO ║──────────────┐
                   │           ╚════╝              │
                ╔═════╗                            ▼
                ║ YES ║                  ┌───────────────────┐
                ╚═════╝                  │ RESULTS.BLOCKED / │
                   │                     │  RESULTS.GRANTED  │
                   ▼                     └───────────────────┘
          ┌────────────────┐
          │ RESULTS.DENIED │◀──────────────────────┐
          └────────────────┘                       │
                   │                               │
                   ▼                               │
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓         ╔════╗
┃ request(PERMISSIONS.ANDROID.CAMERA) ┃         ║ NO ║
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛         ╚════╝
                   │                               │
         Does the user accept                      │
            the request ?                          │
                   │           ╔════╗     Does the user check
                   ├───────────║ NO ║─────"Never ask again" ?
                   │           ╚════╝              │
                ╔═════╗                         ╔═════╗
                ║ YES ║                         ║ YES ║
                ╚═════╝                         ╚═════╝
                   │                               │
                   ▼                               ▼
          ┌─────────────────┐             ┌─────────────────┐
          │ RESULTS.GRANTED │             │ RESULTS.BLOCKED │
          └─────────────────┘             └─────────────────┘
```

### Windows flow

```
   ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
   ┃ check(PERMISSIONS.WINDOWS.WEBCAM) ┃
   ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
                     │
         Is the feature available
              on this device ?
                     │           ╔════╗
                     ├───────────║ NO ║──────────────┐
                     │           ╚════╝              │
                  ╔═════╗                            ▼
                  ║ YES ║                 ┌─────────────────────┐
                  ╚═════╝                 │ RESULTS.UNAVAILABLE │
                     │                    └─────────────────────┘
             Is the permission
               requestable ?
                     │           ╔════╗
                     ├───────────║ NO ║──────────────┐
                     │           ╚════╝              │
                  ╔═════╗                            ▼
                  ║ YES ║                  ┌───────────────────┐
                  ╚═════╝                  │ RESULTS.BLOCKED / │
                     │                     │  RESULTS.GRANTED  │
                     ▼                     └───────────────────┘
            ┌────────────────┐
            │ RESULTS.DENIED │
            └────────────────┘
                     │
                     ▼
  ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
  ┃ request(PERMISSIONS.WINDOWS.WEBCAM) ┃
  ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
                     │
           Does the user accept
              the request ?
                     │           ╔════╗
                     ├───────────║ NO ║──────────────┐
                     │           ╚════╝              │
                  ╔═════╗                            ▼
                  ║ YES ║                   ┌─────────────────┐
                  ╚═════╝                   │ RESULTS.BLOCKED │
                     │                      └─────────────────┘
                     ▼
            ┌─────────────────┐
            │ RESULTS.GRANTED │
            └─────────────────┘
```

## API

### Supported permissions

```js
import {PERMISSIONS} from 'react-native-permissions';

// Android permissions

PERMISSIONS.ANDROID.ACCEPT_HANDOVER;
PERMISSIONS.ANDROID.ACCESS_BACKGROUND_LOCATION;
PERMISSIONS.ANDROID.ACCESS_COARSE_LOCATION;
PERMISSIONS.ANDROID.ACCESS_FINE_LOCATION;
PERMISSIONS.ANDROID.ACTIVITY_RECOGNITION;
PERMISSIONS.ANDROID.ADD_VOICEMAIL;
PERMISSIONS.ANDROID.ANSWER_PHONE_CALLS;
PERMISSIONS.ANDROID.BODY_SENSORS;
PERMISSIONS.ANDROID.CALL_PHONE;
PERMISSIONS.ANDROID.CAMERA;
PERMISSIONS.ANDROID.GET_ACCOUNTS;
PERMISSIONS.ANDROID.PROCESS_OUTGOING_CALLS;
PERMISSIONS.ANDROID.READ_CALENDAR;
PERMISSIONS.ANDROID.READ_CALL_LOG;
PERMISSIONS.ANDROID.READ_CONTACTS;
PERMISSIONS.ANDROID.READ_EXTERNAL_STORAGE;
PERMISSIONS.ANDROID.READ_PHONE_NUMBERS;
PERMISSIONS.ANDROID.READ_PHONE_STATE;
PERMISSIONS.ANDROID.READ_SMS;
PERMISSIONS.ANDROID.RECEIVE_MMS;
PERMISSIONS.ANDROID.RECEIVE_SMS;
PERMISSIONS.ANDROID.RECEIVE_WAP_PUSH;
PERMISSIONS.ANDROID.RECORD_AUDIO;
PERMISSIONS.ANDROID.SEND_SMS;
PERMISSIONS.ANDROID.USE_SIP;
PERMISSIONS.ANDROID.WRITE_CALENDAR;
PERMISSIONS.ANDROID.WRITE_CALL_LOG;
PERMISSIONS.ANDROID.WRITE_CONTACTS;
PERMISSIONS.ANDROID.WRITE_EXTERNAL_STORAGE;

// iOS permissions

PERMISSIONS.IOS.APP_TRACKING_TRANSPARENCY;
PERMISSIONS.IOS.BLUETOOTH_PERIPHERAL;
PERMISSIONS.IOS.CALENDARS;
PERMISSIONS.IOS.CAMERA;
PERMISSIONS.IOS.CONTACTS;
PERMISSIONS.IOS.FACE_ID;
PERMISSIONS.IOS.LOCATION_ALWAYS;
PERMISSIONS.IOS.LOCATION_WHEN_IN_USE;
PERMISSIONS.IOS.MEDIA_LIBRARY;
PERMISSIONS.IOS.MICROPHONE;
PERMISSIONS.IOS.MOTION;
PERMISSIONS.IOS.PHOTO_LIBRARY;
PERMISSIONS.IOS.REMINDERS;
PERMISSIONS.IOS.SIRI;
PERMISSIONS.IOS.SPEECH_RECOGNITION;
PERMISSIONS.IOS.STOREKIT;

// Windows permissions

PERMISSIONS.WINDOWS.APPOINTMENTS;
PERMISSIONS.WINDOWS.BLOCKED_CHAT_MESSAGES;
PERMISSIONS.WINDOWS.BLUETOOTH_GATT;
PERMISSIONS.WINDOWS.BLUETOOTH_RFCOMM;
PERMISSIONS.WINDOWS.CHAT;
PERMISSIONS.WINDOWS.CODE_GENERATION;
PERMISSIONS.WINDOWS.CONTACTS;
PERMISSIONS.WINDOWS.DOCUMENTS_LIBRARY;
PERMISSIONS.WINDOWS.ENTERPRISE_AUTHENTICATION;
PERMISSIONS.WINDOWS.HUMAN_INTERFACE_DEVICE;
PERMISSIONS.WINDOWS.INTERNET_CLIENT;
PERMISSIONS.WINDOWS.INTERNET_CLIENT_SERVER;
PERMISSIONS.WINDOWS.LOCATION;
PERMISSIONS.WINDOWS.MICROPHONE;
PERMISSIONS.WINDOWS.MUSIC_LIBRARY;
PERMISSIONS.WINDOWS.OBJECTS_3D;
PERMISSIONS.WINDOWS.PHONE_CALL;
PERMISSIONS.WINDOWS.PHOTO_LIBRARY;
PERMISSIONS.WINDOWS.POINT_OF_SERVICE;
PERMISSIONS.WINDOWS.PRIVATE_NETWORK_CLIENT_SERVER;
PERMISSIONS.WINDOWS.PROXIMITY;
PERMISSIONS.WINDOWS.RECORDED_CALLS_FOLDER;
PERMISSIONS.WINDOWS.REMOVABLE_STORAGE;
PERMISSIONS.WINDOWS.SHARED_USER_CERTIFICATES;
PERMISSIONS.WINDOWS.USB;
PERMISSIONS.WINDOWS.USER_ACCOUNT_INFORMATION;
PERMISSIONS.WINDOWS.VIDEOS_LIBRARY;
PERMISSIONS.WINDOWS.VOIP_CALL;
PERMISSIONS.WINDOWS.WEBCAM;
```

### Permissions statuses

Permission checks and requests resolve into one of these statuses:

| Return value          | Notes                                                             |
| --------------------- | ----------------------------------------------------------------- |
| `RESULTS.UNAVAILABLE` | This feature is not available (on this device / in this context)  |
| `RESULTS.DENIED`      | The permission has not been requested / is denied but requestable |
| `RESULTS.GRANTED`     | The permission is granted                                         |
| `RESULTS.BLOCKED`     | The permission is denied and not requestable anymore              |

### Getting the result of `PERMISSION.IOS.LOCATION_ALWAYS` on iOS 13 and later

If you request `PERMISSION.IOS.LOCATION_ALWAYS` when `PERMISSION.IOS.LOCATION_WHEN_IN_USE` is granted, the request only resolves _if_ the user selects "Change to Always Allow" from the permission prompt.

If the user selects "Keep Only While Using" from the permission prompt, the request that triggered the prompt will not resolve.

This happens because iOS only informs the library when the authorization status _changes_. Since the authorization status remains the same if the user selects "Keep Only While Using" from the permission prompt, the library doesn't have any way of knowing this and resolving the request.

Subsequent calls to `check`, `checkMultiple`, or `request` with `PERMISSIONS.IOS.LOCATION_ALWAYS` after the user selected "Keep Only While Using" from the permission prompt will return the correct result of `RESULTS.BLOCKED`.

### Methods

```ts
// type used in usage examples
type PermissionStatus = 'unavailable' | 'denied' | 'blocked' | 'granted';
```

#### check

Check one permission status.

```ts
function check(permission: string): Promise<PermissionStatus>;
```

```js
import {check, PERMISSIONS, RESULTS} from 'react-native-permissions';

check(PERMISSIONS.IOS.LOCATION_ALWAYS)
  .then((result) => {
    switch (result) {
      case RESULTS.UNAVAILABLE:
        console.log(
          'This feature is not available (on this device / in this context)',
        );
        break;
      case RESULTS.DENIED:
        console.log(
          'The permission has not been requested / is denied but requestable',
        );
        break;
      case RESULTS.GRANTED:
        console.log('The permission is granted');
        break;
      case RESULTS.BLOCKED:
        console.log('The permission is denied and not requestable anymore');
        break;
    }
  })
  .catch((error) => {
    // …
  });
```

---

#### request

Request one permission.

```ts
type Rationale = {
  title: string;
  message: string;
  buttonPositive?: string;
  buttonNegative?: string;
  buttonNeutral?: string;
};

function request(
  permission: string,
  rationale?: Rationale,
): Promise<PermissionStatus>;
```

```js
import {request, PERMISSIONS} from 'react-native-permissions';

request(PERMISSIONS.IOS.LOCATION_ALWAYS).then((result) => {
  // …
});
```

---

#### checkNotifications

Check notifications permission status and get notifications settings values.

```ts
interface NotificationSettings {
  // properties only availables on iOS
  // unavailable settings will not be included in the response object
  alert?: boolean;
  badge?: boolean;
  sound?: boolean;
  lockScreen?: boolean;
  carPlay?: boolean;
  notificationCenter?: boolean;
  criticalAlert?: boolean;
}

function checkNotifications(): Promise<{
  status: PermissionStatus;
  settings: NotificationSettings;
}>;
```

```js
import {checkNotifications} from 'react-native-permissions';

checkNotifications().then(({status, settings}) => {
  // …
});
```

---

#### requestNotifications

Request notifications permission status and get notifications settings values.

You cannot request notifications permissions on Windows. Disabling or enabling notifications can only be done through the App Settings.

```ts
// only used on iOS
type NotificationOption =
  | 'alert'
  | 'badge'
  | 'sound'
  | 'criticalAlert'
  | 'carPlay'
  | 'provisional';

interface NotificationSettings {
  // properties only availables on iOS
  // unavailable settings will not be included in the response object
  alert?: boolean;
  badge?: boolean;
  sound?: boolean;
  lockScreen?: boolean;
  carPlay?: boolean;
  notificationCenter?: boolean;
  criticalAlert?: boolean;
}

function requestNotifications(
  options: NotificationOption[],
): Promise<{
  status: PermissionStatus;
  settings: NotificationSettings;
}>;
```

```js
import {requestNotifications} from 'react-native-permissions';

requestNotifications(['alert', 'sound']).then(({status, settings}) => {
  // …
});
```

---

#### checkMultiple

Check multiples permissions in parallel.

```ts
function checkMultiple<P extends Permission[]>(
  permissions: P,
): Promise<Record<P[number], PermissionStatus>>;
```

```js
import {checkMultiple, PERMISSIONS} from 'react-native-permissions';

checkMultiple([PERMISSIONS.IOS.CAMERA, PERMISSIONS.IOS.FACE_ID]).then(
  (statuses) => {
    console.log('Camera', statuses[PERMISSIONS.IOS.CAMERA]);
    console.log('FaceID', statuses[PERMISSIONS.IOS.FACE_ID]);
  },
);
```

---

#### requestMultiple

Request multiple permissions in sequence.

```ts
function requestMultiple<P extends Permission[]>(
  permissions: P,
): Promise<Record<P[number], PermissionStatus>>;
```

```js
import {requestMultiple, PERMISSIONS} from 'react-native-permissions';

requestMultiple([PERMISSIONS.IOS.CAMERA, PERMISSIONS.IOS.FACE_ID]).then(
  (statuses) => {
    console.log('Camera', statuses[PERMISSIONS.IOS.CAMERA]);
    console.log('FaceID', statuses[PERMISSIONS.IOS.FACE_ID]);
  },
);
```

---

#### openSettings

Open application settings.

```ts
function openSettings(): Promise<void>;
```

```js
import {openSettings} from 'react-native-permissions';

openSettings().catch(() => console.warn('cannot open settings'));
```

## Migrating from v1.x.x

If you are currently using the version `1.x.x` and would like to switch to `v2.x.x`, the only thing you really need to know is that it's now required to select the wanted permission **per platform**.

```js
// v1.x.x
import Permissions from 'react-native-permissions';

Permissions.request('location', {type: 'whenInUse'});

// v2.x.x
import {Platform} from 'react-native';
import {PERMISSIONS, request} from 'react-native-permissions';

request(
  Platform.select({
    android: PERMISSIONS.ANDROID.ACCESS_FINE_LOCATION,
    ios: PERMISSIONS.IOS.LOCATION_WHEN_IN_USE,
    windows: PERMISSIONS.WINDOWS.LOCATION,
  }),
);
```
