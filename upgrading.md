# upgrading SDK

See [Wiki], [Design Guidelines and Best practices] and [Help Center]  for more detailed informations. you must check [Change Log] .

## Version 2.13
#### Release date: February 22th, 2019

- **Features**
 
     - emphasize on executing init everytime the app runs.
     - support smart v7.
     - better support vast.
     - add OMSDK to debug gyro.
     - support arm64e (new iphones).
     - Remove B4S.

- **Ad Network Mediation Updates**

    - Use new [MngAdsSDK] + *Adapter.a
    - Use new smart v7.
    - Use new [MAdvertiseLocation-v1.1].
    - Remove support for Beacon4Store B4S.

## Upgrading to 2.12.3

- use new [MngAdsSDK]

To check if the interstitial is reday to be showen, you have to call [isInterstitialReady].

```objc
if ([interstitialAdsFactory isInterstitialReady]) {
    [interstitialAdsFactory displayInterstitial];
}

// OR
if ([interstitialAdsFactory isInterstitialReady]) {
    [interstitialAdsFactory showAdFromRootViewController:rootViewController animated:YES];
}

```
___info:___ in some cases the difference between displayInterstitial and showAdFromRootViewController is a little bigger, for example in the case of smart adserver using displayInterstitial will add the the interstitial as a subview in the view of the viewController assigned to the factory, however when using showAdFromRootViewController it will present the interstitial as a viewController which is the case for most other adservers.


___info:___ To test auto-displayin disabled on demo, you have to go to the page interstitial. others interstitials (return background, when change from page to page...) are with auto-displaying.

## Upgrading to 2.12.1

- remove any previous code related to MNGAds managing user's consent (everything related to MAdvertiseConsent class needs to be removed), since MNGAds will be handling the user's consent automatically according to IAB's guidelines.
- use new [MAdvertiseLocation-v1.0].
- use new [MngAdsSDK]


[MAdvertiseLocation-v1.0]: https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/MAdvertiseLocation-v1.0.zip

## Upgrading to 2.12

- Use new MoPub 5.4.0 version, [MoPub Marketplace] + [libMAdvertiseMoPubAdapter.a]
- use new Flurry 9.2.1 version [libFlurryAds] , [libFlurry]
- use new [MngAdsSDK]

## Upgrading to 2.11.1

 - For cocoapod users, OMSDK_Madvertise-x.framework is include into our pod as subspec
 - For manual install OMSDK_Madvertise-x.framework into https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/MNGAds-v2.11.1.zip

## Upgrading to 2.11
 - Add [OMSDK_Madvertise-x.framework] for IAB viewability
 - Add preferredHeight to infeed https://bitbucket.org/mngcorp/mngads-demo-ios/src/master/Demo/MNG-Ads-SDK/InfeedViewController.m
 - Use new AdColony 3.3.4 version, [AdColony.framework]
 - Use new Vectaury 1.6.3 version, [Vectaury.framework]
 - Use new GoogleMobileAds 7.31.0 version [GoogleMobileAds.framework]
 - Use new FacebookAudience 4.28.1 version [FBAudienceNetwork.framework]
 - Use new Flurry 9.0 version [libFlurryAds] , [libFlurry]
 - Use new SmartAdServer 6.10 version [libSmartAdServer.a]
 - Use new AmazonAd SDK 2.2.17.0 version [AmazonAd.framework]
 - Use new MoPub 5.3.0 version, [MoPub Marketplace] + [libMAdvertiseMoPubAdapter.a]
 - Use new [MngAdsSDK] + *Adapter.a

All *Adapter.a available on https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/MNGAds-v2.11.zip

## Upgrading to 2.10

- GDPR: a new class has been introduced to facilitate complying with GDPR MAdvertiseConsent, you will need to create an instance of this new class and pass it to the sdk using the class method setConsentInformation , eg :

```objc

MAdvertiseConsent *consent = [[MAdvertiseConsent alloc]initWithGDPRScope:true.on andConsentStrings:@{@"IAB":"BONlRnIONlRnIAAABAENAAAAAAAAoAA"}];
[MAdvertiseConsent setConsentInformation:consent]

```

for more details check out the header of the new class it s fully documented and [GDPR] doc.

- **Add new AdColony 3.3.0 version, [AdColony.framework]**
- **Add new Vectaury 1.5.2 version, [Vectaury.framework] :**
- Use new Flurry 8.5.0 version [libFlurryAds] , [libFlurry]
- Use new GoogleMobileAds 7.30.0 version [GoogleMobileAds.framework]
- Use new FacebookAudience 4.28.1 version [FBAudienceNetwork.framework]
- Use new SmartAdServer 6.9 version [libSmartAdServer.a]
- Use new [MngAdsSDK]


## Upgrading to 2.9.1

- Use new Flurry 8.4.0 version [libFlurryAds] , [libFlurry]
- Use new MoPub 4.20.1 version, [MoPub Marketplace]
- Use new GoogleMobileAds 7.29.0 version [GoogleMobileAds.framework]
- Use new FacebookAudience 4.28.0 version [FBAudienceNetwork.framework]
- Use new [MngAdsSDK]

## Upgrading to 2.9

 - new delegate method to notify the publisher if the sdk fails its initialization :

```objc
-(void)MNGAdsSDKFactoryDidFailInitializationWithError:(NSError *)error {
    NSLog(@"MNGAds failed initialization");
}
```

- [nativead format], using MNGPreference you can set the preferred adchoices position , although you need to keep in mind that in some cases it might not position it where mentioned since some of the adnetworks won't take this parameter into consideration , so preferably set the preferred position here as well in the didLoad once the request succeeds.

Finally to execute the request you have to call '[loadNativeWithPreferences]'.

```objc
MNGPreference *preferences = MNGPreference *preferences = [[MNGPreference alloc]init];
preferences.preferredAdChoicesPosition = MAdvertiseAdChoiceTopLeft;
[nativeAdsFactory loadNativeWithPreferences:preferences];
```
- **Add new MoPub 4.15.0 version, [MoPub Marketplace] + [libMAdvertiseMoPubAdapter.a]**
- Use new GoogleMobileAds 7.27.0 version [GoogleMobileAds.framework]
- Use new FacebookAudience 4.27.2 version
- Use new [MngAdsSDK] + *Adapter.a



## Upgrading to 2.8.1

- use new Flurry 8.3.4 version [libFlurryAds] , [libFlurry]
- use new AmazonAd SDK 2.2.15.1 version [AmazonAd.framework]
- use new [MngAdsSDK]

## Upgrading to 2.8

- use new GoogleMobileAds 7.26.0 version [GoogleMobileAds.framework]
- use new Flurry 8.3.1 version [libFlurryAds] , [libFlurry]
- use new SmartAdServer 6.7.2 version [libSmartAdServer.a]
- use new [MngAdsSDK]

## Upgrading to 2.7.2

- use new [MngAdsSDK]

## Upgrading to 2.7.1

- use new GoogleMobileAds 7.23.0 version [GoogleMobileAds.framework]
- use new Flurry 8.2.1 version [libFlurryAds] , [libFlurry]
- use new BeaconForStoreSDK 2.2.12 version [BeaconForStoreSDK.framework]
- use new [MngAdsSDK]

## Upgrading to 2.7

- Since BeaconForStoreSDK isnt available by default while using cocoapods, you will need to change mngads's pod line to this:
```
pod "MNGAds",:subspecs => ["MNGAdsFull", "B4S"]
```

- Recently some ads have caused some audio issues: where after the ad is dismissed the entire app becomes muted, and after a thorough investigation we discovered that the issue comes from an adnetwork we currently use and until they fix the issue on their end here s a workaround : what causes the issue is that when a video ad loads it may change the category of AVAudioSession's shared instance, so to avoid this issue you only need to revert (after the ad is dismissed) to the category you initially set, for example :


```
#!objective-c
-(void)adsAdapterInterstitialDisappear:(MNGAdsAdapter *)adsAdapter{

  [[AVAudioSession sharedInstance] setCategory:AVAudioSessionCategoryPlayback error:nil];
  [[AVAudioSession sharedInstance] setActive: YES error: nil];

}
```
###### if you are not using cocoapods to install MNGAds then you should consider upgrading these libraries/frameworks:
- use new FacebookAudience 4.25.0 version 
- use new GoogleMobileAds 7.22.0 version
- use new SmartAdServer 6.7.1 version
- use new BeaconForStoreSDK 2.2.9 version


## Upgrading to 2.6

- Implemented new **eyes tracking** feature in MAdveriseAdserver (MAS) that tracks the user's face to determine if he is really watching an ad (all formats except for native ad) or not , and for how long; this feature is optional, however to enable it, you need to include [umoove.framework] in your project , also you should notice that umoove is a dynamic library so you need to make sure that it s included in **"Embedded Binaries"** as well as **"Linked Frameworks and Librairies"**. Keep in mind that in order to track the user's face, the app will require the use of the device's camera , so dont forget to include **NSCameraUsageDescription** in your info.plist.


###### if you are not using cocoapods to install MNGAds then you should consider upgrading these libraries/frameworks:
- use new FacebookAudience 4.23.0 version [FBAudienceNetwork.framework]
- use new GoogleMobileAds 7.20.0 version [GoogleMobileAds.framework]
- use new Flurry 8.1.0 version [libFlurryAds] , [libFlurry]
- use new BeaconForStoreSDK 2.2.8 version [BeaconForStoreSDK.framework]

## Upgrading to 2.5.3

- use new Flurry 8.0.1 version [libFlurryAds] , [libFlurry]

## Upgrading to 2.5
Dont forget to change your implementation, don't use deprecated methods. 

|Depecated method|New method|
| --- | --- |
|createBanner|loadBanner |
|createBannerInFrame:|loadBannerInFrame:  |
|createBannerInFrame: withPreferences:|loadBannerInFrame: withPreferences:   |
|createInterstitial|loadInterstitial   |
|createInterstitialAutoDisplayed:|loadInterstitialAutoDisplayed:  |
|createInterstitialWithPreferences:|loadInterstitialWithPreferences:   |
|createInterstitialWithPreferences: autoDisplayed:|loadInterstitialWithPreferences: autoDisplayed:   |
|createNative|loadNative   |
|createNativeWithPreferences:|loadNativeWithPreferences:   |
|createInfeedInFrame:|loadInfeedInFrame: |
|createInfeedInFrame: withPreferences:|loadInfeedInFrame:(CGRect)frame withPreferences: |

- use new SmartAdServer 6.6.2 version [libSmartAdServer.a]
- use new B4S 2.2.2 version [BeaconForStoreSDK.framework]
- use new Google-Mobile-Ads-SDK 7.19.1 version [GoogleMobileAds.framework]
- use new FBAudienceNetwork 4.21.0 version [FBAudienceNetwork.framework]

## Upgrading to 2.4

- use new SmartAdServer 6.6.1 version [libSmartAdServer.a]
- use new Flurry 7.10.0 version [libFlurryAds] , [libFlurry]
- use new B4S 2.1.10 version [BeaconForStoreSDK.framework]
- use new Google-Mobile-Ads-SDK 7.18.0 version [GoogleMobileAds.framework]
- use new FBAudienceNetwork 4.20.0 version [FBAudienceNetwork.framework]

## Upgrading to 2.3.4

- use new B4S 6.6 version [BeaconForStoreSDK.framework]
- use new Flurry 7.9.2 version [libFlurryAds] , [libFlurry]


## Upgrading to 2.3.3

 - use new SmartAdServer 6.6 version [libSmartAdServer.a]

## Upgrading to 2.3.2


**This version is ATS-compliant ([App Transport Security]), If you push you submit an app after 1th January 2017, you must use this version.**

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

- add pod dependency for B4S (If you are using cocoapods, you must remove BeaconForStoreSDK.framework/BeaconForStoreSDK, it will be auto-downloaded by cocoapods)

Don't forget to update following libraries :


- [MngAdsSDK]
- [FBAudienceNetwork.framework]
- [GoogleMobileAds.framework]
- [libFlurry_7.8.2.a] [libFlurryAds_7.8.2.a]
- [BeaconForStoreSDK.framework]


## Upgrading to 2.3
Now you can get assets from MNGNativeObject

```objc
__weak NativeAdViewController *weakSelf = self;
    [nativeObject downloadAssetWithType:MAdvertiseAssetTypeAppIcon completition:^(UIImage *image) {
        dispatch_async(dispatch_get_main_queue(), ^{
            if (!weakSelf) {
                return;
            }
            __strong NativeAdViewController *strongSelf = weakSelf;
            strongSelf.iconeImage.image = image;
            strongSelf.nativeView.hidden = NO;
        });
    }];
```

Now you can add beacon for store:

- Get Ebeacon technology to propose to the advertisers to target the users inside the point of sale. 
- An installation base of 12,500 ebeacons ready to track the users.
- An exclusive format in Push notification to the users inside a tabacco shop, press shop, pharmay or mall.

### Initializing Beacons
You have to add libMAdvertiseB4SAdapter.a, BeaconForStoreSDK.framework and BeaconForStoreStorage.bundle to your project.



To access to beacon you have to use the MAdvertiseBeacon singleton. To initialise it you have to call the method initBeacon at application:didFinishLaunchingWithOptions:

```objc
#import <MAdvertiseBeacon.h>
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [MNGAdsSDKFactory initWithAppId:MNG_ADS_APP_ID];
    [[MAdvertiseBeacon singleton]initBeacon];
    //
}
```

### handleNotificationWithUserInfo
To handle beacon local notification, firstable you have to cheack if it is a beacon notification and let MAdvertiseBeacon handle it.

```objc
-(void)application:(UIApplication *)application didReceiveLocalNotification:(UILocalNotification *)notification{
    if ([[MAdvertiseBeacon singleton]userInfoIsBeaconNotification:notification.userInfo]) {
        [[MAdvertiseBeacon singleton]handleNotificationWithUserInfo:notification.userInfo];
    }else{
        //
    }
}


Don't forget to update following libraries :

- [MngAdsSDK]
- [FBAudienceNetwork.framework]
- [libFlurry], [libFlurryAds]
- [libSmartAdServer.a]
- [GoogleMobileAds.framework]

## Upgrading to 2.1.1
### New features
Now you can use new predifined sizes 

```objc
extern MNGAdSize const kMNGAdSizeDynamicBanner; //Small Banner Screen width x 50
extern MNGAdSize const kMNGAdSizeDynamicLeaderboard; //Landscape Banner ipad Screen width x 90
```
libraries

**If you are using cocoapods, you must remove AmazonAd.framework, it will be auto-downloaded by cocoapods**

Don't forget to update following libraries :

 - [MngAdsSDK]
 - [FBAudienceNetwork.framework]
 - [libFlurry], [libFlurryAds]
 - [libSmartAdServer.a]

## Upgrading to 2.1
### New features

Now you can create an [In-Feed Ad format]

```objc
-(BOOL)createInfeedInFrame:(CGRect)frame withPreferences:(MNGPreference*)preferences;
-(BOOL)createInfeedInFrame:(CGRect)frame ;
```

### libraries

 - The following libraries are not required anymore for the sdk

     - Remove [LiveRailSDK.framework]


 - Don't forget to update following libraries :
    - [MngAdsSDK]
    - [FBAudienceNetwork.framework]
    - [AmazonAd.framework]
    - [libFlurry], [libFlurryAds]
    - [libSmartAdServer.a](SDK has been converted to ARC for better memory management)

## Upgrading to v2.x

### adNetworks
Removed:

- Appsfire (now is integrated on [MngAdsSDK])
- Mng Perf (now is integrated on [MngAdsSDK])
- Appnexus (now is integrated on [MngAdsSDK])

Added:

 - [AmazonAd.framework]
 - [LiveRailSDK.framework] 
 - [libFlurryAds_7.3.0.a], [libFlurry_7.3.0.a]
 - [libMNGAdsDFPAdapter.a]
 - [libMNGAdsFacebookAdapter.a]
 - [libMNGAdsSASAdapter.a]
 - [libMNGAmazonAdapter.a]
 - [libMNGFlurryAdapter.a]
 - [libMNGLiveRailAdapter.a]

### Integration

MNGAds v2.0 allow you to choose which adNetworks you will use, the integration process has changed. By default you must add all adapters in order to increase fillrate/revenues

##### Manual integration:

libMNGAds.a is always required and with it you have only Mng Perf and Appsfire works.

To add another adNetwork, you have to add to your project the lib[adNetworkAdapter].a and the adNetwork SDK.

*Example:* To use Smart Ad Server you have to add:

- libMNGAdsSASAdapter.a
- libSmartAdServer.a

**`Important :` If you add just lib[adNetworkAdapter].a, the dispatcher will not use it and if you just add the adNetwork SDK, you will have a compilation error:**
 ```
 References not found
 ```

##### CocoaPods integration

see [Using CocoaPods]

### MediaContainer

With MNGAds v2.0 you can integrate video ads into your Native Ad experience by calling [MNGNAtiveObject setMediaContainer:(UIView *)mediaContainer] and the SDK will add the video or the cover image to your container

```objc
-(void)adsAdapter:(MNGAdsAdapter *)adsAdapter nativeObjectDidLoad:(MNGNAtiveObject *)nativeObject{
    ...
    [nativeObject setMediaContainer:self.container];
    ...
}
```
coverImageUrl still available but it can be `nil`.

## Upgrading to v1.4.1 (Building Against iOS9)

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

You can also edit the plist by adding NSAppTransportSecurity key of dictionary type with a dictionary element of NSAllowsArbitraryLoads of boolean type set to “Yes”.

![ats.png](https://bitbucket.org/repo/aen579/images/32376746-ats.png)

- **v1.4.1 of the SDK supports bitcode**. If you are using earlier versions, you must disable bitcode. **But for now GoogleMobileAds.framework do not support bitcode, therefore you must disable bitcode for your app**

>GoogleMobileAdsSdkiOS-7.4.1/GoogleMobileAds.framework/GoogleMobileAds(GADGestureIdUtil.o)' does not contain bitcode. You must rebuild it with bitcode enabled (Xcode setting ENABLE_BITCODE), obtain an updated library from the vendor, or disable bitcode for this target.

 - **FBAudienceNetwork.framework** and  **libSmartAdServer.a** do not work with **Xcode 6.4**. Therefore, MngAds needs **Xcode 7**.

## Upgrading to v1.4

Now appNexus is available on Cocoapods and pod generate libAppNexusSDK.a, you must remove libANSDK.a old librairy in order to avoid duplicate symbol.

## Upgrading to v1.3.2

The call to the following methods 

```
#!objective-c
-(BOOL)createInterstitialWithPreferences:(MNGPreference*)preferences autoDisplayed:(BOOL)autoDisplyed;  
-(BOOL)createInterstitialAutoDisplayed:(BOOL)autoDisplyed;
```

should be replaced by

```
#!objective-c
-(BOOL)createInterstitialWithPreferences:(MNGPreference*)preferences;
-(BOOL)createInterstitial;
```

## Upgrading to v1.2.1

Bug preference.keyword, now allow empty value if location is setted.

## Upgrading to v1.2

You must add **Appnexus** library. You must setpreference.keyword,if location is setted.(bug fix in v1.2.1)

## Upgrading from v1.0 to v1.1

The following methods have been changed. ```preferredHeight:(CGFloat)preferredHeight``` is now available to more easily resize banners.


```
#!objective-c

(void)adsAdapter:(MNGAdsAdapter *)adsAdapter bannerDidLoad:(UIView *)bannerView preferredHeight:(CGFloat)preferredHeight{
```


instead of


```
#!objective-c

(void)adsAdapter:(MNGAdsAdapter *)adsAdapter bannerDidLoad:(UIView *)bannerView{
```




 [Learn what's new in iOS 9 from Apple]:https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html
 [App Transport Security]:https://developer.apple.com/library/prerelease/ios/technotes/App-Transport-Security-Technote/



[MngAdsSDK]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/
[libSmartAdServer.a]:http://help.smartadserver.com/en/#../../../../specifications/Content/MobileSpecifications/Apps.htm
[FBAudienceNetwork.framework]:https://developers.facebook.com/docs/ios/downloads
[GoogleMobileAds.framework]:https://developers.google.com/mobile-ads-sdk/docs/dfp/ios/download
[Design Guidelines and Best practices]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/guidelines
[Wiki]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/
[Help Center]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/faqhttps://bitbucket.org/mngcorp/mngads-demo-ios/downloads/
[AmazonAd.framework]:https://developer.amazon.com/sdk-download
[LiveRailSDK.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/LiveRailSDK.framework/?at=master
[libFlurryAds]:https://github.com/flurry/ios-AdIntegrationSamples/tree/master/Pods/Flurry-iOS-SDK
[libFlurry]:https://github.com/flurry/ios-AdIntegrationSamples/tree/master/Pods/Flurry-iOS-SDK
[libMNGAdsDFPAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/
[libMNGAdsFacebookAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/
[libMNGAdsSASAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/
[libMNGAmazonAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/
[libMNGFlurryAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/
[libMNGLiveRailAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/MNGAds/libMNGLiveRailAdapter.a?at=master&fileviewer=file-view-default
[Using CocoaPods]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Using%20CocoaPods
[In-Feed Ad format]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Home#markdown-header-infeed
[App Transport Security]:https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW60
[BeaconForStoreSDK.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/d41507a6c8eac3829efd9b05247acac1fcc51f8f/Demo/MNG-Ads-SDK/BeaconForStoreSDK.framework/?at=master

[umoove.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/
[Help Center]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/faq
[Change Log]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/change-log
[nativead format]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/nativead
[MoPub Marketplace]: https://github.com/mopub/mopub-ios-sdk
[libMAdvertiseMoPubAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/
[Vectaury.framework]:https://cdn.vectaury.io/static/sdk/
[AdColony.framework]:https://github.com/AdColony/AdColony-iOS-SDK-3
[GDPR]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/gdpr
[OMSDK_Madvertise-x.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/OMSDK_Madvertise-1.2.4.framework.zip
[MAdvertiseLocation-v1.0]: https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/MAdvertiseLocation-v1.0.zip
[MAdvertiseLocation-v1.1]: https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/MAdvertiseLocation-v1.1.zip