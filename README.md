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

### yarn install
### yarn start
### yarn android




