# Face-Detection-React-Native

setup env

# yarn install
# yarn start
# yarn android

```code
#add faceDetection\android\app\src\main\AndroidManifest.xml
  <uses-permission android:name="android.permission.CAMERA"></uses-permission>
    /* Include this only if you are planning to use the microphone for video recording */
    <application
    ...
      <meta-data 
      android:name="com.google.firebase.ml.vision.DEPENDENCIES"
      android:value="face" />
  # add faceDetection\android\app\build.gradle   
  android {
  defaultConfig {
  ...
  missingDimensionStrategy 'react-native-camera', 'mlkit'
  # add faceDetection\android\build.gradle
  dependencies {
  ...
  classpath 'com.google.gms:google-services:4.3.3'
      
```
