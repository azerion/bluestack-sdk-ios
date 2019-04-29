# ![MNG-Ads-1.png](https://bitbucket.org/repo/aen579/images/3739691856-MNG-Ads-1.png) for IOS

[TOC]

Thanks for taking a look at mngAds! We take pride in having an easy-to-use, flexible monetization solution.

## Need Help?

You can find integration documentation on our [wiki] and additional help documentation on our [developer help site].

## Requirements:
 - Requires **cocoapods 1.2.1**
 - Requires **Xcode 8**.

#### Legacy
 for versions under v2.7 installing the sdk require **git lfs**.

- First Download and install the [git-lfs command line client](https://git-lfs.github.com)
- Then install the Git LFS filters:
```
$ git lfs install —force
```
For more about installing git LFS go to:
https://git-lfs.github.com

## Using CocoaPods
The MngAds SDK is available through [Cocoapods], a popular dependency management system for Objective-C projects.

To download and incorporate the MngAds SDK into your project using Cocoapods, add the following line to your project's podfile:
```ruby
pod "MNGAds"
```
Or:
```ruby
pod "MNGAds/MNGAdsFull"
```

After running `pod install` (if you’re setting up Cocoapods for the first time) or `pod update` (if you’re adding MNGAds to an existing Cocoapods project), it will be ready to use the base MngAds SDK. »

### Troubleshooting

- http://guides.cocoapods.org/using/troubleshooting.html
If you have those build errors:
```
Library not found for -lMNGAds
Header not found for ...
```

You have to check if:
- Header search paths
- Framework search paths
- Library search paths
- Other linker Flags

contains the value ***$(inherited)***

#### App Transport Security Settings
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

On December 21st, Apple announced that they have extended the ATS deadline. Previously, the deadline was January 1, 2017. The new deadline has not yet been announced. Set up the following keys in your app’s info.plist:

```xml
<key>NSAppTransportSecurity</key>
    <dict>
        <key>NSAllowsArbitraryLoads</key>
        <true/>
    </dict>
```
#### cherry-pick install

To add specifics adNetwork.

```ruby
pod "MNGAds",:subspecs => ["AppsFire","Facebook","DFP","SmartAdServer","Amazon","Flurry"]
```

#### MAdvertiseBeacon

Get Ebeacon technology to propose to the advertisers to target the users inside the point of sale. An installation base of 12,500 ebeacons ready to track the users.

```ruby
pod "MNGAds",:subspecs => ["MNGAdsFull"]
```

#### Eyes tracking
>available v2.6

- the face tracking feature was implemented to determine wether the user is watching the ad or not , and for how long (in ms). this feature is optional and disabled by default, to enable it you need to include Umoove either using CocoaPods:
```
pod 'umooveV2framework', :git => 'https://umoove@bitbucket.org/umoove/umooveV2framework.git', :branch =>'master'
```

or manually:
- download [umoove.framework] in your project , also you should notice that umoove is a dynamic library so you need to make sure that it s included in **"Embedded Binaries"** as well as **"Linked Frameworks and Librairies"**.

Keep in mind that in order to track the user's face, the app will require the use of the device's camera , so dont forget to include **NSCameraUsageDescription** in your info.plist.


[wiki]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Home
[developer help site]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/faq
[Cocoapods]:http://cocoapods.org/
[libSmartAdServer.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/sdk/libSmartAdServer.a?at=master&fileviewer=file-view-default
[FBAudienceNetwork.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/FBAudienceNetwork.framework/?at=master
[libANSDK.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/ANSDK/?at=master
[LiveRailSDK.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/LiveRailSDK.framework/?at=master
[AmazonAd.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/AmazonAd.framework/?at=master
[libMAdvertiseB4SAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/MNGAds/libMAdvertiseB4SAdapter.a?at=master&fileviewer=file-view-default
[BeaconForStoreSDK.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/d41507a6c8eac3829efd9b05247acac1fcc51f8f/Demo/MNG-Ads-SDK/BeaconForStoreSDK.framework/?at=master
[BeaconForStoreStorage.bundle]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/BeaconForStoreStorage.bundle/?at=master
[App Transport Security]:https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW33
[umoove.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Umoove.framework/?at=master