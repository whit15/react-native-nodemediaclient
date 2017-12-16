# react-native-nodemediaclient


## 1.install
yarn add react-native-nodemediaclient

## 2.link
react-native link

## 3.Manually modify

### Android
android/build.gradle

```
flatDir{
    dirs "$rootDir/../node_modules/react-native-nodemediaclient/android/libs"
}
```

like this
```
allprojects {
    repositories {
        mavenLocal()
        jcenter()
        maven {
            // All of React Native (JS, Obj-C sources, Android binaries) is installed from npm
            url "$rootDir/../node_modules/react-native/android"
        }
        flatDir{
            dirs "$rootDir/../node_modules/react-native-nodemediaclient/android/libs"
        }
    }
}
```

### iOS

Project -> Build Settings -> Framework Search Paths

Add 
```
$(SRCROOT)/../node_modules/react-native-nodemediaclient/ios/RCTNodeMediaClient
```

## 4.copy NodeMediaClient-SDK
### Android
cp NodeMediaClient-2.3.4.aar node_modules/react-native-nodemediaclient/android/libs/

### iOS
cp NodeMediaClient.framework node_modules/react-native-nodemediaclient/ios/RCTNodeMediaClient/

## 5.permission
## Android 
android/app/src/main/AndroidManifest.xml
```
    <uses-feature android:name="android.hardware.camera"/>
    <uses-feature android:name="android.hardware.camera.autofocus"/>

    <uses-permission android:name="android.permission.CAMERA"/>
    <uses-permission android:name="android.permission.RECORD_AUDIO"/>
    <uses-permission android:name="android.permission.FLASHLIGHT"/>
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>

    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW"/>
    
```
## iOS
Project -> Info

Add
```
Privacy - Camera Usage Description
Privacy - Microphone Usage Description
```

## 6.Example

### NodePlayerView

```
import {  NodePlayerView } from 'react-native-nodemediaclient';

......

<NodePlayerView 
  style={{ height: 200 }}
  ref={(vp) => { this.vp = vp }}
  inputUrl={"rtmp://192.168.0.10/live/stream"}
  scaleMode={"ScaleAspectFit"}
  bufferTime={300}
  maxBufferTime={1000}
  autoplay={true}
/>
```


### NodeCameraView
```
import {  NodeCameraView } from 'react-native-nodemediaclient';

......

<NodeCameraView 
  style={{ height: 400 }}
  ref={(vb) => { this.vb = vb }}
  outputUrl = {"rtmp://192.168.0.10/live/stream"}
  camera={{ cameraId: 1, cameraFrontMirror: true }}
  audio={{ bitrate: 32000, profile: 1, samplerate: 44100 }}
  video={{ preset: 12, bitrate: 400000, profile: 1, fps: 15, videoFrontMirror: false }}
  autopreview={true}
/>

<Button
  onPress={() => {
    if (this.state.isPublish) {
      this.setState({ publishBtnTitle: 'Start Publish', isPublish: false });
      this.vb.stop();
    } else {
      this.setState({ publishBtnTitle: 'Stop Publish', isPublish: true });
      this.vb.start();
    }
  }}
  title={this.state.publishBtnTitle}
  color="#841584"
/>
```
