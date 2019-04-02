# react-native-size-matters-iphonex-xs
[![Build Status](https://travis-ci.org/nirsky/react-native-size-matters.svg)](https://travis-ci.org/nirsky/react-native-size-matters)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)
[![NPM version](https://img.shields.io/npm/v/react-native-size-matters.svg)](https://www.npmjs.com/package/react-native-size-matters)   

A React-Native utility belt for scaling the size your apps UI across different sized devices when building in IPhoneX or XS.


## Installation
```js
npm install --save react-native-size-matters-iphonex-xs
//or:
yarn add react-native-size-matters-iphonex-xs
```

## Motivation
When developing with react-native, you need to manually adjust your app to look great on variety of different screen sizes. That's a tedious job.  
react-native-size-matters provides some simple tooling to make your scaling a whole lot easier.  
But the idea of react-native-size-matters is to develop once on a standard ~5" screen mobile device and then simply apply the provided utils. 
This will make your item's size a little bit different from what you want it to be when building on non standard ~5" screen mobile devices.
In react-native-size-matters-iphonex-xs the standard size is the same with the size of IPhoneX and XS(width: 375, height: 812).
This will enable us to build apps on IPhoneX and XS with no stress. 
So when the desiner made an button with width: 200 , height: 100 in IphoneX or XS you can just style it as width: scale(200) , height: scale(100) and yu can get a perfect design on any device!


## Api
### Scaling Functions
```js
import { scale, verticalScale, moderateScale } from 'react-native-size-matters-iphonex-xs';

const Component = props =>
    <View style={{
        width: scale(30),
        height: verticalScale(50),
        padding: moderateScale(5)
    }}/>;
```


* `scale(size: number)`  
Will return linear scaled result of the provided size, based on your device's screen width.
* `verticalScale(size: number)`  
Will return linear scaled result of the provided size, based on your device's screen height.

* `moderateScale(size: number, factor?: number)`  
Sometimes you don't want to scale everything in a linear manner, that's where moderate scale comes in.  
The cool thing about it is that you can control the resize factor (default is 0.5).  
If normal scale will increase your size by +2X, moderateScale will only increase it by +X, for example:  
➡️ scale(10) = 20  
➡️ moderateScale(10) = 15  
➡️ moderateScale(10, 0.1) = 11  

### ScaledSheet
```js
import { ScaledSheet } from 'react-native-size-matters-iphonex-xs';

const styles = ScaledSheet.create(stylesObject)
```

ScaleSheet will take the same stylesObject a regular StyleSheet will take, plus a special (optional) annotation that will automatically apply the scale functions for you:
* `<size>@s` - will apply `scale` function on `size`.
* `<size>@vs` - will apply `verticalScale` function on `size`.
* `<size>@ms` - will apply `moderateScale` function with resize factor of 0.5 on `size`.
* `<size>@ms<factor>` - will apply `moderateScale` function with resize factor of `factor` on size.

Example:
```js
import { ScaledSheet } from 'react-native-size-matters-iphonex-xs';

const styles = ScaledSheet.create({
    container: {
        width: '100@s', // = scale(100)
        height: '200@vs', // = verticalScale(200)
        margin: 5
    },
    row: {
        padding: '10@ms0.3', // = moderateScale(10, 0.3)
        height: '50@ms' // = moderateScale(50)
    }
});
```
