# IOS SDK Integration

[TOC]

## Overview

BlueStack-SDK provides functionalities for monetizing your mobile application: from premium sales with rich media, video and innovative formats, it facilitates inserting native mobile ads as well all standard display formats. 

- [Smart ads server]
- [Facebook Audience Network]
- [MNG Ad Server] (Mng + AppsFire)
- [Google DFP]
- [AppNexus] (Via Server)
- [MoPub Marketplace]
- [OguryAds]
- [AppLovinSDK]
- [FlurryAds]
- [AdColony]

 

**You can see :** [Our Sample](https://bitbucket.org/mngcorp/mngads-demo-ios/src/master/Demo/), [Change Log] and [Upgrade Guide].



It contains a dispacher that will select an ads server according to the priority and state ([BlueStack state diagram]).

## Requirements

check [Change Log] for  **Xcode version**

#### Legacy
for versions under v2.7 installing the sdk require **git lfs**.


- First Download and install the [git-lfs command line client](https://git-lfs.github.com)
- Then install the Git LFS filters:

```
#!unix

$ git lfs install —force
```
For more about installing git LFS go to:
[LFS Configuration](https://git-lfs.github.com)


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

The BlueStack SDK is available through Cocoapods. see [Using CocoaPods] section.


## Manual Install

- download [BlueStack-SDK], **you must use the according versions of  Ads servers's librairies.**
- drag and drop it in your project
- check that libBlueStack.a exist in "Link Binary With Libraries"

- For manual installation without pod, do not forget to include the "-ObjC" linker flag in "Other Linker Flags" under "Build Settings" in the project file." [see our Faq]


BlueStack SDK needs, these libraries are in demo project :

- [libSmartAdServer.a], use version >=6.3, in used on demo project.
- [FBAudienceNetwork.framework]
- [GoogleMobileAds.framework], use version >=7.8.1, in used on demo project.
- [AmazonAd.framework]
- [libFlurryAds.a]
- [libFlurry.a]
- [MoPub Marketplace]
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

### adNetworkAdapter

**You must add to your project  lib[adNetworkAdapter].a and the adNetwork SDK. You must add all adapters in order to increase fillrate/revenues**

 - [libMNGAdsDFPAdapter.a]
 - [libMNGAdsFacebookAdapter.a]
 - [libMNGAdsSASAdapter.a]
 - [libMNGAmazonAdapter.a]
 - [libMNGFlurryAdapter.a]
 - [libMAdvertiseMoPubAdapter.a]
 - [libMAdvertiseAdColonyAdapter.a]
 - [libMAdvertiseLocationAdapter.a]
 - [libMNGApplovingAdapter.a]
 - [libMAdvertiseBiddingAdapter.a]
 - [libMAdvertiseOguryAdapter.a]


You can see [Installation guide for Swift]

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


## Building Against iOS9

iOS 9 introduces changes that are likely to impact your app and its MngAds integration.

- **[Learn what's new in iOS 9 from Apple]**
- **One of the changes in iOS9 is a default setting that requires apps to make network connections only over SSL ([App Transport Security]).** Therefore Whitelist Ads Servers for Network Requests, mngAds works under https but not all adNetworks on mediation (smartAdserver, appNexus, facebook, ...). if you want to release apps that build against iOS9, you will need to disable ATS in order to ensure all mediation works too.

```
#!objective-c
<key>NSAppTransportSecurity</key>
    <dict>
        <key>NSAllowsArbitraryLoads</key>
        <true/>
    </dict>

```


You can also edit the plist by adding NSAppTransportSecurity key of dictionary type with a dictionary element of NSAllowsArbitraryLoads of boolean type set to �Yes�.

![ats.png](https://bitbucket.org/repo/aen579/images/32376746-ats.png)

- **The SDK supports bitcode**. If you are using earlier versions, you must disable bitcode. **But for now GoogleMobileAds.framework do not support bitcode, therefore you must disable bitcode for your app**

>GoogleMobileAdsSdkiOS-7.4.1/GoogleMobileAds.framework/GoogleMobileAds(GADGestureIdUtil.o)' does not contain bitcode. You must rebuild it with bitcode enabled (Xcode setting ENABLE_BITCODE), obtain an updated library from the vendor, or disable bitcode for this target.

 - **FBAudienceNetwork.framework** and  **libSmartAdServer.a** do not work with **Xcode 6.4**. Therefore, MngAds needs **Xcode 7**.
 - 
## Sample Application

Included is a [BlueStack sample app] to use as example and for help on BlueStack integration. This basic application allows users to test our differents formats.

#### Important note:
just run pod install after cloning the demo


[ARC]:https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/AutomaticReferenceCounting.html
[link]:http://www.tutorialspoint.com/ios/ios_location_handling.htm
[Smart ads server]:http://help.smartadserver.com/fr/Default.htm#../../../../specifications/Content/MobileSpecifications/Apps.htm
[Mng-perf]:https://bitbucket.org/mngcorp/mngperf-demo-ios
[Google DFP]:https://developers.google.com/mobile-ads-sdk/download#download
[Facebook Audience Network]:https://developers.facebook.com/docs/ios?locale=fr_FR
[BlueStack-SDK]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/
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
[Using CocoaPods]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Using%20CocoaPods
[BlueStack state diagram]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/diagram
[Installation guide for Swift]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Swift
[Design Guidelines and Best practices]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/guidelines
[MNG Ad Server]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/

[AmazonAd.framework]:https://developer.amazon.com/sdk-download
[LiveRailSDK.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/LiveRailSDK.framework/?at=master
[libFlurryAds.a]:https://github.com/flurry/ios-AdIntegrationSamples/tree/master/Pods/Flurry-iOS-SDK
[libFlurry.a]:https://github.com/flurry/ios-AdIntegrationSamples/tree/master/Pods/Flurry-iOS-SDK
[Native Ads guidelines]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/nativead
[libMNGAdsDFPAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/
[libMNGAdsFacebookAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/
[libMNGAdsSASAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/
[libMNGAmazonAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/
[libMNGFlurryAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/
[libMAdvertiseAdColonyAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/
[libMAdvertiseLocationAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/
[libMAdvertiseMoPubAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/
[see our Faq]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/faq#markdown-header--objc-linker-flag-required

[libMNGApplovingAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/
[libMAdvertiseBiddingAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/
[libMAdvertiseOguryAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/

[App Transport Security]:https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW60
[extended the ATS deadline]:https://developer.apple.com/news/?id=12212016b&1482372961

[MoPub Marketplace]: https://github.com/mopub/mopub-ios-sdk

[FlurryAds]: https://developer.yahoo.com/flurry/docs/
[OguryAds]: https://www.ogury.com
[AppLovinSDK]:https://www.applovin.com
[AdColony]: http://adcolony.com

