# IOS Bluestack-SDK-Core SDK Integration

[TOC]

## Overview

BlueStack-SDK-Core provides functionalities for monetizing your mobile application: from premium sales with rich media, video and innovative formats, it facilitates inserting native mobile ads as well all standard display formats. 


 

**You can see :** [Our Sample](https://bitbucket.org/mngcorp/mngads-demo-ios/src/master/Demo/), [Change Log] and [Upgrade Guide].



It contains a dispacher that will select an ads server according to the priority and state ([BlueStack state diagram]).

## Requirements

check [Change Log] for  **Xcode version**



## Version
See [Change Log] and [Upgrade Guide].

## Guidelines

See [Design Guidelines and Best practices]

## Demo

Once you cloned/downloaded the repository, make sure to run pod install before trying to run our Demo.

## Help and Troubleshooting

[Help Center]
Answers to frequently asked questions


## Using CocoaPods

The BlueStack SDK Core is available through Cocoapods. see [Using CocoaPods] section.


## Manual Install

- download [BlueStack-SDK-Core],*
- drag and drop it in your project
- check that libBlueStack.a exist in "Link Binary With Libraries"

- For manual installation without pod, do not forget to include the "-ObjC" linker flag in "Other Linker Flags" under "Build Settings" in the project file." [see our Faq]


BlueStack SDK Core needs, these libraries are in demo project :

- CoreGraphics.framework
- QuartzCore.framework
- SystemConfiguration.framework
- MediaPlayer.framework
- CoreMotion.framework
- GLKit framework
- JavaScriptCore
- AdSupport.framework
- StoreKit.framework
- CoreLocation.framework
- Accelerate/Accelerate.h Framework
- CoreMedia
### Bluestack-SDK-Core

you can use Bluestack-SDK-Core only without the adNetworks SDKs 

```ruby
pod "Bluestack-SDK-Core"
```

## App Transport Security Settings
[App Transport Security] improves privacy and data integrity by ensuring your app’s network connections employ only industry-standard protocols and ciphers without known weaknesses. This helps instill user trust that your app does not accidentally leak transmitted data to malicious parties.

MNGAds SDK (with Mediation) are now ATS-compliant, but a small percentage of creatives (near to zero) not directly hosted on our platform are not.

If you must make an exception for a reason, we recommend that you minimize it by only setting the NSAllowsArbitraryLoadsInWebContent and NSAllowsArbitraryLoadsForMedia keys,

```xml
<key>NSAppTransportSecurity</key>
    <dict>
        <key>NSAllowsArbitraryLoadsForMedia</key>
            <true/>
        <key>NSAllowsArbitraryLoadsInWebContent</key>
            <true/>
    </dict>
```

On December 21st, Apple announced that they have [extended the ATS deadline]. Previously, the deadline was January 1, 2017. The new deadline has not yet been announced.
Set up the following keys in your app’s info.plist:



```
#!objective-c
<key>NSAppTransportSecurity</key>
    <dict>
        <key>NSAllowsArbitraryLoads</key>
        <true/>
    </dict>
```

  - ## Sample Application

Included is a [BlueStack sample app] to use as example and for help on BlueStack integration. This basic application allows users to test our differents formats.

#### Important note:
just run pod install after cloning the demo


##  Configuring the SDK

### Init the SDK

You have to init the SDK in AppDelegate.m in application:didFinishLaunchingWithOptions:
**This must be executed everytime you run the App**

```objc
// AppDelegate.m
#import "MNGAdsSDKFactory.h"
...
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
[MNGAdsSDKFactory initWithAppId:@"YOUR_APP_ID"];
...
}
```

### Initialisation Delegate

MNGAds SDK is configured by server or from last configuration. So in first run after installation, initialisation take some time before be done .

To check out if the SDK is initialized or not, you have to use `[MNGAdsSDKFactory isInitialized]`. To know when the SDK has finished Initializing you have to use MNGAdsSDKFactoryDelegate.

```objc
// AppDelegate.h
#import "MNGAdsSDKFactory.h"

@interface AppDelegate : UIResponder <UIApplicationDelegate,MNGAdsSDKFactoryDelegate>



// AppDelegate.m
...
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [MNGAdsSDKFactory initWithAppId:@"YOUR_APP_ID"];
    if([MNGAdsSDKFactory isInitialized] == NO){
        [MNGAdsSDKFactory setDelegate:self];
    }
    ...
}

-(void)MNGAdsSDKFactoryDidFinishInitializing{
    if (YOUR_APP_IS_READY_TO_SHOW_AD) {
        INIT_FACTORIES_AND_USE_THEM_TO_SHOW_ADS;
    }
}

-(void)MNGAdsSDKFactoryDidFailInitializationWithError:(NSError *)error {
    NSLog(@"MNGAds failed initialization");
}
```

### Timeout
The time given to the ad view to download the ad data. After this time, the dispacher stops the ad server running (with failure) and move to the next.
the default timeout is 1s.

```objc
adsFactory = [[MNGAdsSDKFactory alloc]init];
adsFactory.timeout = 3;
```
### isBusy
Before making a request you have to check that factory not busy (handling old request).

Ads factory is busy means that it has not finished the previous request yet.

isBusy will be setted to true when factory start handling request.

isBusy will be setted to false when factory finish handling request.

**example:**

```objc
if (bannerAdsFactory.isBusy) {
NSLog(@"Ads Factory is busy");
}else{
NSLog(@"Ads Factory is not busy");
}
[bannerAdsFactory loadBannerInFrame:CGRectMake(0, 0, 320, 50)]
if (bannerAdsFactory.isBusy) {
NSLog(@"Ads Factory is busy");
}else{
NSLog(@"Ads Factory is not busy");
}
```
**Log:**

```shell
$Ads Factory is not busy
$Ads Factory is busy
```


### Preferences Object
Preferences object is an optional parameter that allow you select ads by user info.
informations that you can set are:

- age : age of user
- location : geographical position of the user. *Important:* your application can be rejected by Apple if you use the device's location *only* for advertising.
- language : language of user (ISO code)
- gender : gender of user
- keyWord : Use free-form key-values when you want to pass targeting values dynamically into an ad tag based on information you collect from your users. You can also use free-form key-values when there are too many possible values to define in advance. Separator in case of multiple entries is **;**.
- content url : URL for content related to your app (url must be a string which length not exceed 512 caracters).
- preferredAdChoicesPosition : set the preferred adchoices position , although you need to keep in mind that in some cases it might not position it where mentioned since some of the adnetworks wont take this parameter into consideration , so preferably set the preferred position here as well in the didLoad once the request succeeds.


```
#!objective-c

key=value;key2=value2
```


```objc
#import "MNGPreference.h"
...
MNGPreference * preference = [[MNGPreference alloc]init];
preference.age = 25;
preference.language = @"fr";
preference.keyword = @"brand=myBrand;category=sport";//Separator in case of multiple entries is ; key=value
preference.gender = MNGGenderFemale;
preference.location = [[CLLocation alloc]initWithLatitude:48.876 longitude:10.453];
[preference setContentUrl:@"your content url"];
[bannerAdsFactory loadBannerInFrame:CGRectMake(0, 0, 320, 50)withPreferences:preference];
```
`Note`: this [link] can help you to get device location.

### Error Handling
@available v2.5
Whenever an Ad fails to load, its correspondent delegate would be invoked providing an NSError object describing what went wrong, what s new in v2.5 and later versions is that we added a new Enum representing the codes of different errors along with a clear description , the different types of error can be found in top of MNGAdsSDKFactory header file :

![MAdvertiseError.png](https://bitbucket.org/repo/aen579/images/3273016750-MAdvertiseError.png)

the different errors are pretty much self explanatory , and here s and example use just to remove any ambiguity there might be on how to use it :

```objc

-(void)adsAdapter:(MNGAdsAdapter *)adsAdapter nativeObjectDidFailWithError:(NSError *)error{
    NSLog(@"%@",error.localizedDescription); //will log the error's description
    if (error.code == MAdvertiseErrorWrongPlacement) {
        myFactory.placementId = @"Insert the correct placement";
        [myFactory loadNative];
    }
}

```

### Memory managment
When you have finished your ads plant you must free the memory.

When using [ARC] it will be done automatically. Otherwise you have to call "releaseMemory".
###### ARC
```objc
[adsFactory releaseMemory];//optional
adsFactory = nil;
```
But we recommand to release memory in order to avoid **crashes with a "EXC_BAD_ACCESS" ** for some adNetworks.

###### No ARC

```objc
[adsFactory releaseMemory];//required
[adsFactory release];
adsFactory = nil;
```

###### Avoid crashes

Some adNetwork does not using **A**utomatic **R**eference **C**ounting, so you have to mange MNGAdsFactory pointer specially fo interstitial.

 - **Do not call releaseMemory on viewDidDisappear**

 - you have to call releaseMemory before removing pointer from current instance.

The simplest way is:

- Calling releaseMemory before setting your property:

```objc
    [intersFactory releaseMemory];
    intersFactory = otherFactory;// Or
    intersFactory = [[MNGAdsFactory alloc]init];// Or
    intersFactory = nil;
```
- Calling releaseMemory at the dealloc of delegate$


```objc
    -(void)dealloc{
        [intersFactory releaseMemory];
        intersFactory = nil;
    }
```

## Select an ad format

BlueStack SDK core offers a number of different ad formats :

- Banner [Integration guides](https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/banner)

- Interstitial [Integration guides](https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/interstitial)

- Native Ads [Integration guides](https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/nativead)

- Rewarded Video [Integration guides](https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/rewarded-video-ios)

- Infeed [Integration guides](https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/infeed)


[ARC]:https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/AutomaticReferenceCounting.html
[link]:http://www.tutorialspoint.com/ios/ios_location_handling.htm
[Smart ads server]:http://help.smartadserver.com/fr/Default.htm#../../../../specifications/Content/MobileSpecifications/Apps.htm
[Mng-perf]:https://bitbucket.org/mngcorp/mngperf-demo-ios
[Google DFP]:https://developers.google.com/mobile-ads-sdk/download#download
[Facebook Audience Network]:https://developers.facebook.com/docs/ios?locale=fr_FR
[BlueStack-SDK-Core]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/
[BlueStack sample app]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD?at=master
[appsfire]:https://github.com/appsfire/Appsfire-iOS-SDK
[Help Center]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/faq
[Change Log]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/change-log
[Upgrade Guide]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/upgrading
[AppNexus]:http://www.appnexus.com/fr
[libANSDK]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/AppNexusSDK/?at=master

[libSmartAdServer.a]:http://help.smartadserver.com/en/#../../../../specifications/Content/MobileSpecifications/Apps.htm
[FBAudienceNetwork.framework]:https://developers.facebook.com/docs/ios/downloads
[GoogleMobileAds.framework]:https://developers.google.com/mobile-ads-sdk/docs/dfp/ios/download
[libAppsfireSDK.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/AppsfireSDK/?at=master
[libMng-perf.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/Mng-perf/?at=master
[Using CocoaPods]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Using-CocoaPods
[BlueStack state diagram]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/diagram
[Installation guide for Swift]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Swift
[Design Guidelines and Best practices]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/guidelines
[MNG Ad Server]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/