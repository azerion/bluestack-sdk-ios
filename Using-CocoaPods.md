![mad_AdNetworkMediation_rgb_small.png](https://bitbucket.org/repo/GyRXRR/images/3981639300-mad_AdNetworkMediation_rgb_small.png) for IOS


[TOC]

Thanks for taking a look at BlueStack! We take pride in having an easy-to-use, flexible monetization solution.

## Need Help?

You can find integration documentation on our [wiki] and additional help documentation on our [developer help site].

## Requirements:
 - Requires **cocoapods 1.2.1**
 - Requires **Xcode 8**.

## Using CocoaPods
The BlueStack-SDK is available through [Cocoapods], a popular dependency management system for Objective-C projects.

To download and incorporate the BlueStack-SDK  into your project using Cocoapods, add the following line to your project's podfile:

```ruby
pod "BlueStack-SDK"
```
Or:

```ruby
pod "BlueStack-SDK/Full"
```

After running `pod install` (if you’re setting up Cocoapods for the first time) or `pod update` (if you’re adding BlueStack-SDK to an existing Cocoapods project), it will be ready to use the base BlueStack-SDK. »

### Troubleshooting

- http://guides.cocoapods.org/using/troubleshooting.html
If you have those build errors:
```
Library not found for -lBlueStack-SDK
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

BlueStack-SDK (with Mediation) are now ATS-compliant, but a small percentage of creatives (near to zero) not directly hosted on our platform are not.

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
pod "BlueStack-SDK",:subspecs => ["FBAudienceNetwork","Google-Mobile-Ads-SDK","Smart-Display-SDK","In-App-Bidding","OguryAds","CriteoPublisherSdk","AmazonPublisherServicesSDK","MAdvertiseLocation"]

```
#### MadvertiseLocation(Since v2.12.1)

You will just need to specify the subspec for Madvertise Location since it s not included by default like so :

```
  pod "BlueStack-SDK",:subspecs => ["MAdvertiseLocation"]
```
* **Enable Background Mode** :
You need to tick the box "Location updates" in the "Capabilities" of your target.

* **requestAuthorization** :

Ask the user to share their location data (popup) with the +requestAuthorization: function:
 Put this line where it makes the most sense for your app user experience. This will trigger a permission request popup. If you already asked thoses permissions elsewhere in your app, you don't need to call it (if you do, it will have no impact).


[wiki]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Home
[developer help site]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/faq
[Cocoapods]:http://cocoapods.org/
[libSmartAdServer.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/sdk/libSmartAdServer.a?at=master&fileviewer=file-view-default
[FBAudienceNetwork.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/FBAudienceNetwork.framework/?at=master
[libANSDK.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/ANSDK/?at=master
[LiveRailSDK.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/LiveRailSDK.framework/?at=master
[AmazonAd.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/AmazonAd.framework/?at=master
[App Transport Security]:https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW33
[umoove.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Umoove.framework/?at=master