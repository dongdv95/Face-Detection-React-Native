# Face-Detection-React-Native

##setup env

## Add the folowing to project level build.gradle:
```js
buildscript {
  dependencies {
  // Add this line
  classpath 'com.google.android.gms:strict-version-matcher-plugin:1.2.1' // <--- you might want to use different version
  }
}
```
## add to the bottom of android/app/build.gradle file
```js
apply plugin: 'com.google.android.gms.strict-version-matcher-plugin'

android {
  defaultConfig {
  ...
  missingDimensionStrategy 'react-native-camera', 'mlkit'
```
## add faceDetection\android\app\src\main\AndroidManifest.xml
```code

  <uses-permission android:name="android.permission.CAMERA"></uses-permission>
    /* Include this only if you are planning to use the microphone for video recording */
    <application
    ...
      <meta-data 
      android:name="com.google.firebase.ml.vision.DEPENDENCIES"
      android:value="face" />
      
```

# For IOS
## Add dependency towards react-native-camera in your Podfile with subspecs using one of the following:
```code
pod 'react-native-camera', path: '../node_modules/react-native-camera', subspecs: [
  'FaceDetectorMLKit'
]
```
## Add permissions with usage descriptions to your app Info.plist:
```code
<!-- Required with iOS 10 and higher -->
<key>NSCameraUsageDescription</key>
<string>Your message to user when the camera is accessed for the first time</string>

<!-- Required with iOS 11 and higher: include this only if you are planning to use the camera roll -->
<key>NSPhotoLibraryAddUsageDescription</key>
<string>Your message to user when the photo library is accessed for the first time</string>

<!-- Include this only if you are planning to use the camera roll -->
<key>NSPhotoLibraryUsageDescription</key>
<string>Your message to user when the photo library is accessed for the first time</string>

<!-- Include this only if you are planning to use the microphone for video recording -->
<key>NSMicrophoneUsageDescription</key>
<string>Your message to user when the microphone is accessed for the first time</string>
```

### yarn install
### yarn start
### yarn android




