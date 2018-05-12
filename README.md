
# React Native Barcode Scanners <a href="https://opensource.org/licenses/MIT"><img src="https://img.shields.io/badge/License-MIT-blue.svg"></a>

A barcode scanner component created based on [react-native-camera](https://github.com/react-native-community/react-native-camera) and [react-native-image-picker](https://github.com/react-community/react-native-image-picker), Supported Android and IOS

This component has been created for a simple use of barcode scanner with some customizations, like so:


Demo1 | Demo2
----- | ----
<img title="Demo1" src="https://s1.ax1x.com/2018/05/13/CDAqd1.jpg"> | <img title="Demo2" src="https://s1.ax1x.com/2018/05/13/CDAbZR.jpg">

## Get Started

### Supported
* iOS
* Android

### Install

`npm install react-native-barcode-scanners --save`

#### Android Installation

`react-native link`
`react-native link react-native-camera`

IMPORTANT NOTE: In the use of react-native-camrea gradle upgrade caused Android package error, reference [here](https://github.com/react-native-community/react-native-camera/issues/1490)

#### iOS Installation
##### step1. react-native-lewin-qrcode
1.In the XCode's "Project navigator", right click on your project's Libraries folder ➜ Add Files to <...>
2.Go to node_modules ➜ react-native-lewin-qrcode ➜ ios ➜ select QrCode.xcodeproj

##### step2. react-native-camera
1. In XCode, in the project navigator, right click Libraries ➜ Add Files to [your project's name]
2. Go to node_modules ➜ react-native-camera and add RNCamera.xcodeproj
3. Expand the RNCamera.xcodeproj ➜ Products folder
4. In XCode, in the project navigator, select your project. Add libRNCamera.a to your project's Build Phases ➜ Link Binary With Libraries
5. Click RNCamera.xcodeproj in the project navigator and go the Build Settings tab. Make sure 'All' is toggled on (instead of 'Basic'). In the Search Paths section, look for Header Search Paths and make sure it contains both $(SRCROOT)/../../react-native/React and $(SRCROOT)/../../../React - mark both as recursive.
6.For iOS 10+, Add the NSPhotoLibraryUsageDescription, NSCameraUsageDescription, NSPhotoLibraryAddUsageDescription and NSMicrophoneUsageDescription (if allowing camera) keys to your Info.plist with strings describing why your app needs these permissions. Note: You will get a SIGABRT crash if you don't complete this step
```
    <key>NSPhotoLibraryAddUsageDescription</key>
    <string>$(PRODUCT_NAME) would like to save photos to your photo gallery</string>
```
More about the configuration of react-native-camera [here](https://github.com/react-native-community/react-native-camera)

##### step3. react-native-image-picker
1.In the XCode's "Project navigator", right click on your project's Libraries folder ➜ Add Files to <...>
2.Go to node_modules ➜ react-native-image-picker ➜ ios ➜ select RNImagePicker.xcodeproj
3.Add RNImagePicker.a to Build Phases -> Link Binary With Libraries
4.For iOS 10+, Add the NSPhotoLibraryUsageDescription, NSCameraUsageDescription, NSPhotoLibraryAddUsageDescription and NSMicrophoneUsageDescription (if allowing camera) keys to your Info.plist with strings describing why your app needs these permissions. Note: You will get a SIGABRT crash if you don't complete this step
```
    <key>NSPhotoLibraryUsageDescription</key>
    <string>$(PRODUCT_NAME) would like access to your photo gallery</string>
    <key>NSCameraUsageDescription</key>
    <string>$(PRODUCT_NAME) would like to use your camera</string>
    <key>NSPhotoLibraryAddUsageDescription</key>
    <string>$(PRODUCT_NAME) would like to save photos to your photo gallery</string>
```
More about the configuration of react-native-image-picker [here](https://github.com/react-community/react-native-image-picker)

### Usage example
```javascript
'use strict';
import React, { Component } from 'react';
import {
  Alert,
} from 'react-native';

import BarcodeScanner from 'react-native-barcode-scanners'

export default class App extends Component {

  constructor(props){
    super(props)
  }
  onBarCodeRead(res){
    Alert.alert('HINT', res.data)
  }
  onReadBarCodeByGalleryFailure(){
    Alert.alert('HINT', 'Not found barcode!')
  }
  componentDidMount () {}
  render() {
    return (
      <BarcodeScanner
        onReadBarCodeByGalleryFailure={()=>this.onReadBarCodeByGalleryFailure.call(this)}
        onBarCodeRead={(data)=>this.onBarCodeRead.call(this, data)}
      />
    )
  }
}
```

## Props
### Native callbacks props
#### onBack
Function to be called when click back triangular icon, when isEnableTopBar is true(the isEnableTopBar true by default).
```javascript
onBack(){
    // do something
}
```
#### onBarCodeRead
Function to be called when native code emit onScanCode, when barcode is detected.
```javascript
onBarCodeRead(res){
    let barcode = res.data
    Alert.alert('HINT', barcode)
}
```
#### onBarCodeReadByGalleryStart
Function to be called when Start identifying photo album barcode.
```javascript
onBarCodeReadByGalleryStart(res){
    // do something
}
```
#### onReadBarCodeByGalleryFailure
Function to be called when Failed to recognize the barcode of the album image (Cause: The picture no't barcode or system error)
```javascript
onReadBarCodeByGalleryFailure(res){
    Alert.alert('HINT', 'Not found barcode!')
}
```
### Options props

Prop                   | Type    | Optional | Default                        | Description
---------------------- | ------- | -------- | ------------------------------ | -----------
isEnableAnimationScan  | bool    | Yes      | true                           | Whether to enable scan animation
isEnableMask           | bool    | Yes      | true                           | Whether to enable background mask
isEnableTopBar         | bool    | Yes      | true                           | Whether to enable the top section
isEnableScanBorder     | bool    | Yes      | true                           | Whether to enable the scanned box border
isEnableDiscernPicture | bool    | Yes      | true                           | Whether to enable the identification picture barcode from the album
Title                  | string  | Yes      | 'Title'                        | TopBar title
hintScanText           | string  | Yes      | 'Put the barcode into the box' | Scan position hint text
hintOrText             | string  | Yes      | 'OR'                           | More operating hint text
hintPictureGalleryText | string  | Yes      | 'Choose photo gallery'         | Hint text for select barcode from photo album 
hintOpenLightText      | string  | Yes      | 'ON'                           | Hint text for open light
hintCloseLightText     | string  | Yes      | 'OFF'                          | Hint text for close light
RenderTopBar           | element | Yes      |                                | Top bar custom react component
topBarBackgroundColor  | string  | Yes      | 'rgba(0,0,0,0.1)'              | Top bar background color
maskColor              | string  | Yes      | 'rgba(0,0,0,0.4)'              | The mask background color 
RenderScanLine         | element | Yes      |                                | The scan line custom react component
scanBoxSize            | number  | Yes      | WINDOW_WIDTH * 0.6             | The scan box size
scanBorderColor        | string  | Yes      | 'rgba(250,250,250,0.3)'        | The scan box border color
scanAngleColor         | string  | Yes      | 'rgba(250,250,250,0.4)'        | The scan angle background color
scanAngleWidth         | number  | Yes      | 28                             | The scan angle width
scanAngleHeight        | number  | Yes      | 5                              | The scan angle height
lightBackgroundColor   | string  | Yes      | '#181D20'                      | The flashlight block background color

## License
[React Native Barcode Scanner is MIT licensed.](https://opensource.org/licenses/MIT)