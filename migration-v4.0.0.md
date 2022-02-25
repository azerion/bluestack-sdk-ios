# Migration guide to v4.0.0
[TOC]

From 22th February 2022, Updated the SDK from a lib.a to a .xcframework.

## Requirements
-  Required apps to build against Xcode 12.2 or higher.
-  Target iOS 12.2 or higher
-  CocoaPods 1.9.0 or higher is now required for CocoaPod installations.
-  Added an arm64 simulator slice to allow testing on simulators for Apple Silicon Mac platforms.


##  Podfile BlueStackSDK

In order to import the latest version of the new BlueStackSDK, you must update the Cocoapods dependency in the Podfile of your application. Now, you have to change the version to 4.0.0

```ruby
pod "BlueStack-SDK",'4.0.0' ,:subspecs => ["Full","MAdvertiseLocation"]
```
  
**Duplicate symbols when framework target has a static dependency**

To fix Cocoapods bug : 

 - you will need  add the ruby Script [BlueStackDuplicatedFrameworksRemover]  in our Project 

 - you will need  loadd the ruby Script  [BlueStackDuplicatedFrameworksRemover] in our Podfile 

 - update   remove_duplicated_frameworks('Pods-MNG-Ads-SDK-Demo', installer) with our target name  **"remove_duplicated_frameworks('Pods-OURTARGETNAME', installer)"**

example Podfile: 
 
```ruby
source 'https://github.com/CocoaPods/Specs.git'

platform :ios, '12.2'

use_frameworks!
load 'BlueStackDuplicatedFrameworksRemover.rb'


target 'MNG-Ads-SDK-Demo' do

   pod "BlueStack-SDK" ,'4.0.0' ,:subspecs => ["Full","MAdvertiseLocation"]

   pod 'MAdvertiseCMP' ,'58'
   pod 'Firebase/Crashlytics' ,'8.11.0'
   pod 'Firebase/Analytics' ,'8.11.0'

   
end


post_install do |installer|
    remove_duplicated_frameworks('Pods-MNG-Ads-SDK-Demo', installer)
end

```
## Import the BlueStackSDK

Before initializing the BlueStackSDK you will need to change the import of the new name of the header file to the path xcframework:

##### Old import

```ruby
#import "Protocols.h"
#import "MNGPreference.h"
#import "MNGNAtiveObject.h"
#import "MNGAdsSDKFactory.h"
#import "MNGAdsAdapter.h"
#import "MAdvertiseRewardedVideoAd.h"
#import "MAdvertiseReward.h"
#import "MAdvertiseInfeedFrame.h"

```

##### New import

```ruby
#import  <BlueStackSDK/Protocols.h>
#import  <BlueStackSDK/MNGPreference.h>
#import  <BlueStackSDK/MNGNAtiveObject.h>
#import  <BlueStackSDK/MNGAdsSDKFactory.h>
#import  <BlueStackSDK/MNGAdsAdapter.h>
#import  <BlueStackSDK/MAdvertiseRewardedVideoAd.h>
#import  <BlueStackSDK/MAdvertiseReward.h>
#import  <BlueStackSDK/MAdvertiseInfeedFrame.h>

```

[BlueStackDuplicatedFrameworksRemover]: https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/BlueStackDuplicatedFrameworksRemover.rb