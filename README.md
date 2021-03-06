# react-native-communications-zmt

### 功能：

实现打电话、发短信、打开系统通讯录功能

### 使用步骤：

#### 一、链接Communication库

参考：https://reactnative.cn/docs/0.50/linking-libraries-ios.html#content

##### 手动添加：

1、添加`react-native-communications-zmt`插件到你工程的`node_modules`文件夹下

2、添加`Communication`库中的`.xcodeproj`文件在你的工程中

3、点击你的主工程文件，选择`Build Phases`，然后把刚才所添加进去的`.xcodeproj`下的`Products`文件夹中的静态库文件（.a文件），拖到`Link Binary With Libraries`组内。

##### 自动添加：

```
npm install react-native-communications-zmt --save 
或
yarn add react-native-communications-zmt

react-native link
```

#### 二、开发环境配置

如果是`iOS10`需要在`plist`文件中进行如下配置：

![](http://upload-images.jianshu.io/upload_images/2093433-106317e5bcad4b7b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
<key>NSContactsUsageDescription</key>  
<string>App需要您的同意,才能访问通讯录</string>  
```

#### 三、简单使用

##### 方法

Event Name | Returns | Notes 
------ | ---- | -------
call | message | 打电话
messageNumberWithMessage | message | 发短信
openContacts |name,phone | 打开通讯录

##### js文件

```
/**
* Sample React Native App
* https://github.com/facebook/react-native
* @flow
*/

import React, { Component } from 'react';
import {
AppRegistry,
StyleSheet,
Text,
View,
Dimensions,
AlertIOS,
ScrollView,
TouchableHighlight,
NativeAppEventEmitter
} from 'react-native';

import Communication from 'react-native-communications-zmt';


export default class CommunicationView extends Component {


call() {
Communication.call('10000',(message) => {
if (message) {
AlertIOS.alert(message);
}
});
}

messageNumberWithMessage() {
Communication.messageNumberWithMessage('10000','发短信给10000',(message) => {
if (message) {
AlertIOS.alert(message);
}
});
}

openContacts() {
Communication.openContacts((name,phone) => {
if (phone) {
// AlertIOS.alert(name);
AlertIOS.alert(phone);
}
});
}



render() {
return (
<ScrollView contentContainerStyle={styles.wrapper}>

<TouchableHighlight
style={styles.button} underlayColor="#f38"
onPress={this.call}>
<Text style={styles.buttonTitle}>打电话</Text>
</TouchableHighlight>


<TouchableHighlight
style={styles.button} underlayColor="#f38"
onPress={this.messageNumberWithMessage}>
<Text style={styles.buttonTitle}>发短信</Text>
</TouchableHighlight>

<TouchableHighlight
style={styles.button} underlayColor="#f38"
onPress={this.openContacts}>
<Text style={styles.buttonTitle}>打开通讯录</Text>
</TouchableHighlight>


</ScrollView>
);
}
}

const styles = StyleSheet.create({
wrapper: {
paddingTop: 60,
paddingBottom: 20,
alignItems: 'center',
},
pageTitle: {
paddingBottom: 40
},
button: {
width: 200,
height: 40,
marginBottom: 10,
borderRadius: 6,
backgroundColor: '#f38',
alignItems: 'center',
justifyContent: 'center',
},
buttonTitle: {
fontSize: 16,
color: '#fff'
}

});
```

效果展示

![](http://upload-images.jianshu.io/upload_images/2093433-d072bdfe543132f0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

