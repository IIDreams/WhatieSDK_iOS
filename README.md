
![](https://img.shields.io/badge/platform-iOS-red.svg) ![](https://img.shields.io/badge/language-Objective--C-orange.svg) [![CocoaPods compatible](https://img.shields.io/cocoapods/v/WhatieSDK.svg?style=flat)](https://cocoapods.org/pods/WhatieSDK) ![](https://img.shields.io/badge/license-MIT%20License-brightgreen.svg)  

## WahtieSDK Version 1.3.0 updated at 2018-11-02

```
What's new:

2018-11-02：

1.smartConfig：
We are very sorry about the wifi connection issues!
In order to find the problem and improve SDK,monitoring MQTT message of smartConfig is necessary.
Please refer to 5.1 and Note.

2.Some of APIs for timer and Countdown have been changed,including adding a timer and adding a timing countdown.
Please refer to 7.1 and 8.1.

3.APIs for RGB light and monochrome light bulbs have been published. Please refer to 6 and 7 and 9.2.

History:

2018-08-19：
Rename room of device. Please refer to 6.6.

2018-08-15：
"Unable to update device status" may not be appear if mobile network well.

2018-07-28：
Update some of the information returned.

```
## 1.Features Overview

WhatieSDK is a SDK provided by ATI TECHNOLOGY (WUHAN) CO.,LTD. for the 3rd party accessing to our ATI IoT cloud platform easily and quickly. Using this SDK, developers can do almost all function points on electrical outlets and RGBW or monochrome bulbs, such as user registration/login/logout, smart configuration, add/share/remove devices, device control, timing countdown, timer, etc. 

[![](https://github.com/ATI-Wuhan/WhatieSDKDemo_iOS/blob/master/images/1small.PNG)](https://github.com/ATI-Wuhan/WhatieSDKDemo_iOS/blob/master/images/1.PNG)
[![](https://github.com/ATI-Wuhan/WhatieSDKDemo_iOS/blob/master/images/2small.PNG)](https://github.com/ATI-Wuhan/WhatieSDKDemo_iOS/blob/master/images/2.PNG)
[![](https://github.com/ATI-Wuhan/WhatieSDKDemo_iOS/blob/master/images/3small.PNG)](https://github.com/ATI-Wuhan/WhatieSDKDemo_iOS/blob/master/images/3.PNG)
[![](https://github.com/ATI-Wuhan/WhatieSDKDemo_iOS/blob/master/images/4small.PNG)](https://github.com/ATI-Wuhan/WhatieSDKDemo_iOS/blob/master/images/4.PNG)
[![](https://github.com/ATI-Wuhan/WhatieSDKDemo_iOS/blob/master/images/5small.PNG)](https://github.com/ATI-Wuhan/WhatieSDKDemo_iOS/blob/master/images/5.PNG)
[![](https://github.com/ATI-Wuhan/WhatieSDKDemo_iOS/blob/master/images/6small.PNG)](https://github.com/ATI-Wuhan/WhatieSDKDemo_iOS/blob/master/images/6.PNG)
[![](https://github.com/ATI-Wuhan/WhatieSDKDemo_iOS/blob/master/images/7small.PNG)](https://github.com/ATI-Wuhan/WhatieSDKDemo_iOS/blob/master/images/7.PNG)


**Note:** For all function points, no any backend development on cloud platform is needed for integrating the SDK into your APP. You just do all your work in your APP side. 



## 2.Preparation

### Sign up a developer account
Sign up a 3rd party developer account at ATI cloud platform to create self-developed products, create function points, and so on.

**Note:** We have signed up an account for SAKAR, which has been emailed to SAKAR. SAKAR can just skip this step.

### Obtain appId and secretKey
Go to Development Platform - Application Management - Create a new application to obtain an `appId` and `secretKey` to initialize SDKs (for both Android and iOS).
[![](https://github.com/ATI-Wuhan/WhatieSDKDemo_iOS/blob/master/images/appId.png)](https://github.com/ATI-Wuhan/WhatieSDK_iOS/blob/master/images/appId.png)

**Note:** We have applied appId and secretKey for SAKAR, which has been emailed to SAKAR. SAKAR can just skip this step.

### SDK Demo
SDK Demo is a complete APP incorporating the main flows and operations such as registration, login, sharing, feedback, network configuration and device control, etc. The Demo code can be used as a good reference for the 3rd party development. [Download link](https://github.com/ATI-Wuhan/WhatieSDKDemo_iOS)



## 3.SDK Integration

### Requirements
* iOS 8 or later
* Xcode 9 or later

### Use CocoaPods for rapid integration (Note: version 8.0 or above is supported)
Add the following content in file `Podfile`:
```objc
platform :ios, '8.0'   
target 'Your_Project_Name' do       
    pod 'WhatieSDK',:git => 'https://github.com/ATI-Wuhan/WhatieSDK_iOS.git'  
end
```
[![](https://github.com/ATI-Wuhan/WhatieSDKDemo_iOS/blob/master/images/pod.png)](https://github.com/ATI-Wuhan/WhatieSDK_iOS/blob/master/images/pod.png)

Execute the command `pod install` in the project’s root directory to begin the integration procedure.
For instructions of CocoaPods, please refer to [CocoaPods Guides](https://guides.cocoapods.org)

### Alternative method: Manual Install with Framework
You can also add WhatieSDK as a framework to your project or workspace.

1. Download the WhatieSDK.framework
2. Open your project in Xcode, then drag and drop `WhatieSDK.framework` into your project.
3. Include WhatieSDK wherever you need it with `#import <WhatieSDK/WhatieSDK.h>`

### Initialize SDK
You can add the following code to the project file PrefixHeader.pch:
`#import <WhatieSDK/WhatieSDK.h>`
Open file `AppDelegate.m`, and use the `appId` and `secretKey`, obtained from the development platform, in the `[AppDelegate application:didFinishLaunchingWithOptions:]` method to initialize SDK, as below:

```objc
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

    //Init WhatieSDK
    [[EHOMESDK shareInstance] startWithAppId:appId secretKey:secretKey];
    
    //your code...
}
```

Now, all the preparing work has been done.

### Example code conventions
The following example code, unless otherwise stated, all instances are located in the implementation file of the `ViewController` class.

```objc
@interface ViewController : UIViewController  

@end

  @implementation ViewController  

//All example code are located here...  

@end
```



## 4.User Management

The SDK provides user management functions, such as user registration, user login, user logout, login password update, and change nickname.

**Note:**
1. all other information on user management procedure is not needed for SDK. 
2. The user email and password ciphertext will be also stored in our cloud platform. 
3. No any backend development (on cloud side) is needed for integrating the SDK into your APP.

All user-related functions can be found in the EHOMEUserModel class (singleton).

### 4.1 User registration
**Note:** The following example code is a successful call of the registration method. After registration, user logins automatically, and it is unnecessary to call the login method anymore.

#### Email registration
No verification code is required during email registration. Users may register their accounts directly using their emails:

```objc
-(void)registerByEmail{     
    [[EHOMEUserModel shareInstance] registerByEmail:@"your_email" password:@"your_password" success:^(id responseObject) {
        NSLog(@"register success");            
    } failure:^(NSError *error) {
        NSLog(@"register failed");
    }];
}
```

### 4.2 User login
Upon a successful call, the user’s session will be stored locally by the SDK. When the app is launched next time, the user is logged in by default, and no more login action is required.

#### Email login

```objc
-(void)loginByEmail{     
    [[EHOMEUserModel shareInstance] loginByEmail:@"your_email" password:@"your_password" success:^(id responseObject) {
        NSLog(@"login success = %@", responseObject);
    } failure:^(NSError *error) {
        NSLog(@"login failed = %@", error);
    }];
}
```

### 4.3 Password reset by users

#### Password reset with an email address
If you forget your password, you can reset your password with the e-mail address consisting of two steps:
* Sending a verification code to the mailbox

```objc
-(void)sendVerifyCodeByEmail{
    [[EHOMEUserModel shareInstance] sendVerifyCodeByEmail:@"your_email" success:^(id responseObject) {
        NSLog(@"Verify Code sent success. res = %@", responseObject);            
    } failure:^(NSError *error) {
        NSLog(@"Verify Code sent filed. error = %@", error);
    }];
}
```

* The verification code received is then used to reset the password

```objc
-(void)resetPasswordByEmail {
    [[EHOMEUserModel shareInstance] resetPasswordByEmail:@"your_email" newPassword:@"your_password" code:@"verify_code" success:^(id responseObject) {
        NSLog(@"Reset password success. res = %@", responseObject);
    } failure:^(NSError *error) {
        NSLog(@"Reset password failed. error = %@", error);
    }];
}
```

### 4.4 Password reset by old password
If you just want to update your password, you can reset your password with the e-mail address and old password

```objc
-(void)resetPasswordByOldPassword{
    [[EHOMEUserModel shareInstance] resetPasswordByOldPassword:@"your_old_password" newPassword: @"your_new_password" email:@"your_email" success:^(id responseObject) {
        NSLog(@"Reset Password Success = %@", responseObject);
    } failure:^(NSError *error) {
        NSLog(@"Reset Password Failed = %@", error);
    }];
}
```

### 4.5 Update a user’s device list
Using the `[[EHOMEUserModel shareInstance] syncDeviceWithCloud…]` method will update the user’s current device list `deviceArray`.

Each of the deviceArray is `<EHOMEDeviceModel * >`. And the device properties are in `EHOMEDeviceModel.h`.

```objc
-(void)reloadDeviceList{
    [[EHOMEUserModel shareInstance] syncDeviceWithCloud:^(id responseObject) {
        NSLog(@"Get my devices successful : %@", responseObject);
        NSLog(@"deviceArray : %@", [EHOMEUserModel shareInstance].deviceArray);
    } failure:^(NSError *error) {
        NSLog(@"Get my devices failed : %@", error);
    }];
}
```

### 4.6 Handle device list changes
Listen for the `EHOMEUserNotificationDeviceArrayChanged` notification, so that a notification can be received in the case of any changes to the device list `[EHOMEUserModel shareInstance].deviceArray` data.

```objc
//register notice EHOMEUserNotificationDeviceArrayChanged 
-(void)viewDidLoad{
    //Register Notice
    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(reloadData) name: EHOMEUserNotificationDeviceArrayChanged object:nil];
}  

-(void)reloadData{     
    //Refresh UI here 
}

  -(void)dealloc{ 
    [[NSNotificationCenter defaultCenter] removeObserver:self]; 
}
```

### 4.7 Update a user’s received shared device list
Using the `[[EHOMEUserModel shareInstance] syncSharedDeviceWithCloud…]` method will update the user’s current shared device list `sharedDeviceArray`.

```objc
-(void)reloadSharedDeviceList{
    [[EHOMEUserModel shareInstance] syncSharedDeviceWithCloud:^(id responseObject) {
        NSLog(@"Get shared devices successful : %@", responseObject);
        NSLog(@"sharedDeviceArray : %@", [EHOMEUserModel shareInstance].sharedDeviceArray);
    } failure:^(NSError *error) {
        NSLog(@"Get shared devices failed : %@", error);
    }];
}
```

### 4.8 Handle a user’s received shared device list changes
Listen for the `EHOMEUserNotificationSharedDeviceArrayChanged` notification, so that a notification can be received in the case of any change to the device list `[EHOMEUserModel shareInstance].sharedDeviceArray` data.

```objc
//register notice EHOMEUserNotificationSharedDeviceArrayChanged 
-(void)viewDidLoad{
    //Register Notice
    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(reloadData) name: EHOMEUserNotificationSharedDeviceArrayChanged object:nil];
}  

-(void)reloadData{ 
    //Refresh UI here
}

  -(void)dealloc{     
    [[NSNotificationCenter defaultCenter] removeObserver:self]; 
}
```

### 4.9 Update the nickname
The user can change user name by update the nickname method, as below:
```objc
-(void)updateNickname:(NSString *)nickname{     
    [[EHOMEUserModel shareInstance] updateNickname:@"your_nickname" success:^(id responseObject) {
        NSLog(@"update nickname success. res = %@", responseObject);                
    } failure:^(NSError *error) {
        NSLog(@"update nickname failed. error = %@", error);
    }];
}
```

### 4.10 Logout
The user can logout the APP by the method as below: 
```objc
-(void)loginOut{
    [[EHOMEUserModel shareInstance] loginOut:^(id responseObject) {
        NSLog(@"logOut success = %@", responseObject);
    } failure:^(NSError *error) {
        NSLog(@"logOut failed = %@", error);
    }];
}
```



## 5. SmartConfig and Device Init
### 5.1 SmartConfig
The device uses the EHOMESmartConfig singleton function to perform network configuration as below:
```objc
-(void)smartConfig{
    [[EHOMESmartConfig shareInstance] startSmartConfigWithSsid:ssid bssid:bssid password:password success:^(id responseObject) {
        NSLog(@"Smart config success = %@", responseObject);
        
        //Operation of smart config success
        
        //Note:Congratulations！Your device has been connected to Wifi.But it could not be work until it is registered.
        Then,you should monitor the MQTT message in function named "viewDidload".
        
        self.isSmartconfig = YES;
        
    } failure:^(NSError *error) {
        NSLog(@"Smart config failed = %@", error);
        
        dispatch_async(dispatch_get_main_queue(), ^{
        
            //Operation of smart config failed
            [self showFailAlert];
        });
    }];
```
**Note:**
You should monitor MQTT messages in "viewDidLoad" while smartConfig.After smartConfig success,the device will start to register.If protocal of MQTT message is equal to 9,the device registered successfully and it can be used.The method of monitoring MQTT messages is as follows:
```objc
-(void)viewDidLoad{

/*you code*/

//smartConfig
[[EHOMEMQTTClientManager shareInstance] setMqttBlock:^(NSString *topic, NSData *data) {
        NSDictionary *MQTTMessage = [NSJSONSerialization JSONObjectWithData:data options:NSJSONReadingMutableContainers error:nil];
        
        if ([[MQTTMessage allKeys] containsObject:@"protocol"]) {
            NSInteger protocol = [[MQTTMessage objectForKey:@"protocol"] integerValue];
            
            if (protocol == 10) {
                
            }else if (protocol == 9) {
                //if protocol == 9,device registered successful.
                
                //Operation of registration success
                self.isRegister = YES;
                
            }
        }
    }];
}
```

Stop SmartConfig

After smartConfig is started, the app will broadcast the WiFi network information continuously (until smartConfig succeeds or times out). To cancel the operation, the ```[[EHOMESmartConfig shareInstance] stopSmartConfig]``` method should be called.

```objc
-(void)stopSmartConfigAction{
    
    [[EHOMESmartConfig shareInstance] stopSmartConfig];
}

```


### 5.2 Device Init
After finishing the SmartConfig procedure, the device should be initialized with devId and device name.
```objc
-(void)getStarted{
    [[EHOMESmartConfig shareInstance] getStartedWithDevId:@"your_device_devId" deviceName:@"your_deviceName" success:^(id responseObject) {
        NSLog(@"GET STARTED Success = %@", responseObject);
    } failure:^(NSError *error) {
        NSLog(@"GET STARTED Failed = %@", error);
    }];
}  
```

## 6. Device Control

### 6.1 OnOff device
You can turn on/off the device by the following method:
```objc
-(void)updateDeviceStatus:(BOOL)status{
    [self.device updateDeviceStatus:@"your_status" success:^(id responseObject) {
        NSLog(@"update device status success. res = %@", responseObject);
    } failure:^(NSError *error) {
        NSLog(@"update device status failed. error = %@", error);
    }];
}
```

### 6.2 Rename device
The device name can be renamed by:
```objc
-(void)updateDeviceName:(NSString *)deviceName{
    [self.device updateDeviceName:@"your_deviceName" success:^(id responseObject) {
        NSLog(@"update device name success. res = %@", responseObject);            
    } failure:^(NSError *error) {
        NSLog(@"update device name failed. error = %@", error);
    }];
}
```

### 6.3 Remove device
The device can be removed if you don't need this device, no matter its your own or its a device shared to you. If the removed device is your own, the device is reset to network-pending state.
```objc
-(void)removeDevice{
    [self.device removeDevice:^(id responseObject) {
        NSLog(@"remove device success = %@", responseObject);
    } failure:^(NSError *error) {
        NSLog(@"remove device failed = %@", error);
    }];
}
```

### 6.4 Share device by email
The device can be shared to your friend by:
```objc
-(void)shareDeviceByEmail{
    [self.device shareDeviceByEmail:@"your_friend_email" success:^(id responseObject) {
        NSLog(@"share device success. res = %@", responseObject);
    } failure:^(NSError *error) {
        NSLog(@"share device failed. error = %@", error);
    }];
}
```

### 6.5 Share device by scan code
This method should be called when scanning the QR code.
```objc
[EHOMEDeviceModel sharedDeviceWithAdminUserId:[shareUerIdStr intValue] sharedUserId:[EHOMEUserModel getCurrentUser].id deviceId:[shareDeviceIdStr intValue] timestamp:dTime suucessBlock:^(id responseObject) {
    NSLog(@"share device success = %@", responseObject);
} failBlock:^(NSError *error) {
    NSLog(@"share device failed = %@", error);
}];
```

### 6.6 Remove shares
Please refer to 6.3 Remove device.

### 6.7 Rename room of device
```objc
-(void)updateDeviceRoomName{
    [self.device updateRoomName:@"your_room_name" success:^(id responseObject) {
        //update room name success
    } failure:^(NSError *error) {
        //update room name failed
    }];
}
```



## 7. Timer
**Important Note:** loops: @“0000000”, each bit, 0: off, 1: on, representing from left to right: Sunday Saturday Friday Thursday Wednesday Tuesday Monday

### 7.1 Add a timer
Set a timer to operate the device on some specific time. Your operation on the device will take effect once the time of the timer arrives.   
@param loops   
@param time : the time user set to, like: @"18:57"   
@param status : the status of the device is to be when timer arrives  
@param tag : the name of the timer  
@param stripMode : if the device is not power strip,This parameter is set to int 0

```objc
-(void)addTimer{
    [self.device addTimerWithLoops:loops time:self.time status:self.status tag:self.tag stripMode:self.stripType success:^(id responseObject) {
        NSLog(@"add timer success, response = %@", responseObject);
            
    } failure:^(NSError *error) {
        
        NSLog(@"add timer failed, error = %@", error);
    }];
}
```

### 7.2 Update a timer
You can update/modify the assigned timer by:  
```objc
-(void)updateTimer{
    [self.timer updateTimerWithLoops:loops time:self.time status:self.status tag:self.tag deviceType:self.device.device.product.productType success:^(id responseObject) {
        NSLog(@"update timer success, response = %@", responseObject);
    } failure:^(NSError *error) {
        NSLog(@"update timer failed, error = %@", error);
    }];
}
```

### 7.3 Update timer status
Update the status of a specified timer under a specified device, i.e., 0: off, 1: on, using the following method:

```objc
-(void)updateTimerStatus:(BOOL)status{
    [self.timer updateTimerStatus:@"your_timerStatus" success:^(id responseObject) {
        NSLog(@"update timer status success.response = %@", responseObject);        
    } failure:^(NSError *error) {
        NSLog(@"update timer status failed.error = %@", error);
    }];
}
```

### 7.4 Remove a timer
Delete a specified timer under a specified device by:

```objc
- (void)removeTimer {     
    [self.timer removeTimer:^(id responseObject) {
        NSLog(@"remove timer success.response = %@", responseObject);
    } failure:^(NSError *error) {
        NSLog(@"remove timer failed.error = %@", error);
    }];
}
```

### 7.5 Obtain all timers
Obtain all timers under a specified device by:

```objc
- (void)getAllTimers{
    [self.device getAllTimers:^(id responseObject) {
        NSLog(@"get all timers success,timers = %@", responseObject);
    } failure:^(NSError *error) {
        NSLog(@"get all timers failed,error = %@", error);
    }];
}
```

## 8. Timing Countdown
You can create a timing countdown for a specific device.
 
### 8.1 Add a timing countdown
Your operation on the device will take effect once timing countdown is finished.  
Light has no timing and countdown function.  
@param IsPowerStrips : if the device is outlet,set to no     
@param clockId : if the device is outlet,set to int 0  
@param status : the status of the device is to be when countdown is finished   
@param duration : the duration of timing countdown. The unit is second, such as 10seconds; if 10 minutes, the value is 600.

```objc
-(void)addTimingCountdown{
    [self.device addTimingCountdownWithIsPowerStrips:false clockId:0 Duration:duration status:!isOn success:^(id responseObject) {
        NSLog(@"add timing countdown success. res = %@", responseObject);
    } failure:^(NSError *error) {
        NSLog(@"add timing countdown failed. error = %@", error);
    }];
}
```

### 8.2 Obtain a timing countdown
Get a timing countdown under a specific device, and then, you can show its value in the APP.
```objc
-(void)getTimingCountdown{
    [self.device getTimingCountdown:^(id responseObject) {
        NSLog(@"get timing countdown success. res = %@", responseObject);
        EHOMETimer *timer = responseObject;
    } failure:^(NSError *error) {
        NSLog(@"get timing countdown failed. error = %@", error);
    }];
}  
```

### 8.3 Update a timing countdown
Once you update a timing countdown, it will become a new one. Please refer to 8.1 Add a timing countdown.


## 9. Monochrome Light and RGB Light Bulbs

### 9.1 On/Off

Please refer to Chapter 6.1 On/Off the device.


### 9.2 Monochrome Light Bulbs
You can change brightness for a specific monochrome light bulb by the following method:

```objc
-(void)brightnessSliderValueChange:(UISlider *)slider{
    
    NSLog(@"brightness slider value = %f", slider.value);

    
    [self.device updateIncandescentLightBrightness:(int)slider.value success:^(id responseObject) {
        
    } failure:^(NSError *error) {
        
    }];    
}
```

### 9.3 RGB Light Bulbs

#### 9.3.1 Update RGB Light Bulb Color
You can update the color for a specific RGB light bulb by the following method:

```objc
-(void)updateRGBLightColor{
    
        NSString *rgb = [NSString stringWithFormat:@"%d_%d_%d", r, g, b];


        [self.device updateRGBLightColorWithRGB:rgb success:^(id responseObject) {
            
        } failure:^(NSError *error) {
            
        }];
}
```

#### 9.3.2 Update RGB Light Bulb Brightness
You can update the brightness for a specific RGB light bulb by the following method:

```objc
-(void)rgbBrightnessSliderValueChange:(UISlider *)slider{
    
    NSLog(@"rgb brightness slider value = %f", slider.value);
    
    [self.device updateRGBLightBrightness:(int)slider.value success:^(id responseObject) {
        
    } failure:^(NSError *error) {
        
    }];
}
```


### 9.4 Smooth/Stream Light Mode for the RGB Light Bulbs

#### 9.4.1 Update Smooth/Stream Light Color
You can update the color for a specific smooth/stream light by the following method:

```objc
-(void)updateStreamLightColor{

    [self.device updateStreamLightColorWithRGB1:@"your_rgb_color_1" RGB2:@"your_rgb_color_2" RGB3:@"your_rgb_color_3" RGB4:@"your_rgb_color_4" success:^(id responseObject) {
        
    } failure:^(NSError *error) {
        
    }];

}
```

#### 9.4.2 Update Smooth/Stream Light Duration
You can update the time duration for a specific smooth/stream light by the following method:

```objc
-(void)updateStreamLightDuration{

    
    [self.device updateStreamLightDuration:(int)@"your_duration" success:^(id responseObject) {
        
    } failure:^(NSError *error) {
        
    }];

}
```

#### 9.4.3 Update Smooth/Stream Light Brightness
You can update the brightness for a specific smooth/stream light by the following method:

```objc
-(void)updateStreamLightBrightness{

    [self.device updateStreamLightBrightness:(int)@"your_brightness" success:^(id responseObject) {
        
    } failure:^(NSError *error) {
        
    }];
}
```


### 9.5 Monochrome/Incandescent Light for RGB Light Bulbs
You can change the brightness for a specific monochrome/incandescent light for the RGB light bulb by the following method:
This method is as the same as changing brightness of the monochrome light bulb.
```objc
-(void)brightnessSliderValueChange:(UISlider *)slider{
    
    NSLog(@"brightness slider value = %f", slider.value);

    
    [self.device updateIncandescentLightBrightness:(int)slider.value success:^(id responseObject) {
        
    } failure:^(NSError *error) {
        
    }];    
}
```


## Welcome to contact us:
* iOS Contributors: Yiran Ding, IIDreams, Linjun Chen
* Email : zhouwei20150901@icloud.com, whatie@qq.com

## LICENSE
WhatieSDK uses MIT LICENSE.
