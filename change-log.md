## Change log and release notes for the MngAds SDK for iOS.

See [Wiki], [Design Guidelines and Best practices] and [Help Center]  for more detailed informations.


you must check [Upgrade Guide]. You need to keep all Ad Network jars up to date. 

## Version 2.6
#### Release date: June 23th, 2017

- Implemented new **eyes tracking** feature in MAdvertiseAdserver (MAS) that tracks the user's face to determine if he is really watching the ad or not , and for how long. You need to include [umoove.framework] in your project
- New infeed ad format in mngadserver (MAS).
- New features in debug gyro.
- Disable scroll in some banners.
- Fix possible bug where the cascade would be blocked without returning a valid ad nor a fail error.
- Edit impression requirements.
- Fix banner size bug.
- Fix clickUrl issue.
- Remove spaces from keywords.


- use new FacebookAudience 4.23.0 version [FBAudienceNetwork.framework]
- use new GoogleMobileAds 7.20.0 version [GoogleMobileAds.framework]
- use new Flurry 8.1.0 version [libFlurryAds] , [libFlurry]
- use new BeaconForStoreSDK 2.2.8 version [BeaconForStoreSDK.framework]


## Version 2.5.3
#### Release date: April 24th, 2017

- fix supported architectures issue where you get differents warnings about different adapters not supporting some architectures,in some cases it goes as far as saying that some adapters cannot be found during runtime.

- use new Flurry 8.0.1 version [libFlurryAds] , [libFlurry]


## Version 2.5.1
#### Release date: April 19th, 2017

- use new FBAudienceNetwork v4.22.0 version [FBAudienceNetwork.framework] (Fixed a critical bug that the image ad content is not rendered in FBMediaView.)


## Version 2.5
#### Release date: April 17th, 2017

 - Some methods in MNGAdsFactory are now deprecated and will be removed in next version:

| Depecated method | New method |
| --- | --- |
| createBanner() | loadBanner() |
| createBanner(MNGFrame frame) | loadBanner(MNGFrame frame)  |
|createBanner(MNGPreference preference)|loadBanner(MNGPreference preference)   |
|createBanner(MNGFrame frame, MNGPreference preference)|loadBanner(MNGFrame frame, MNGPreference preference) |
|createInterstitial()|loadInterstitial()   |
|createInterstitial(boolean autoDisplay)|loadInterstitial(boolean autoDisplay)  |
|createInterstitial(MNGPreference preference)|loadInterstitial(MNGPreference preference)   |
|createInterstitial(MNGPreference preference, boolean autoDisplay)|loadInterstitial(MNGPreference preference, boolean autoDisplay)   |
|createNative()|loadNative()   |
|createNative(MNGPreference preference)|loadNative(MNGPreference preference)   |
|createNativeCollection(int requestedAdNumber)|loadNativeCollection(int requestedAdNumber)  |
|createNativeCollection(int requestedAdNumber, MNGPreference preference)|loadNativeCollection(int requestedAdNumber, MNGPreference preference)   |
|createInfeed()|loadInfeed() |
|createInfeed(MNGFrame frame)|loadInfeed(MNGFrame frame) |
|createInfeed(MNGPreference preference)|loadInfeed(MNGPreference preference) |
|createInfeed(MNGFrame frame, MNGPreference preference)|loadInfeed(MNGFrame frame, MNGPreference preference) |

- MAdvertiseError : in case of fail, the didFail delegate method will be invoked with an MAdvertiseError, you want to check which error was invoked by checking its code and description and matching it with the predefined MAdvertiseErrors (see Error Handling in the documentation for more info).
- persisent seenAd : seenAd is now managed in the sdk cache without life time.
- native ad adChoice : adserver can return an adchoice view for native ad.
- clarify doc about native ad registerViewForInterraction.
- add crashlitycs in MngAdsDemo. 
 - Fixed bugs:
   - Null values in Request : don't send the parameter to the adNetwork if it is null or empty.
   - Inall : fix dfp custom targetting and key words.

Don't forget to update following libraries :

- [MngAdsSDK]
- [FBAudienceNetwork.framework]
- [GoogleMobileAds.framework]
- [BeaconForStoreSDK.framework]

## Version 2.4.1
#### Release date: March 22th, 2017

 - fix crash for appsfire banner

Don't forget to update following libraries :

- [MngAdsSDK]

## Version 2.4
#### Release date: March 10th, 2017

- use new SmartAdServer 6.6.1 version [libSmartAdServer.a]
- use new Flurry 7.10.0 version [libFlurryAds] , [libFlurry]
- use new B4S 2.1.10 version [BeaconForStoreSDK.framework]
- use new Google-Mobile-Ads-SDK 7.18.0 version [GoogleMobileAds.framework]
- use new FBAudienceNetwork 4.20.0 version [FBAudienceNetwork.framework]
- improve AppsFire cache managment
- add support for vast inline
- new Interstitiel management pattern: once you have an interstitiel loaded all new requests to create a new one (w/ same placement and viewController) will hand out the already loaded interstitiel instead of creating a new request.
- new inall targetting
- badge in the nativeAd is customizable now using the method:

```
    [_nativeObject updateBadgeTitle:@"newBadgeTitle"];

```

>note that the new method returns a BOOL indicating if the update was successful or not.

- contentUrl: new attribut in MNGPreference : now you can pass to the sdk an URL for content related to your app (url must be a string which length do not exceed 512 characters)
- persistent capping : capping is now managed on cache.
- memory management improvement.
- fix minor bugs.

## Version 2.3.4
#### Release date: January 27th, 2017

- use new B4S 6.6 version [BeaconForStoreSDK.framework]
- use new Flurry 7.9.2 version [libFlurry] [libFlurryAds]
- improve AppsFire cache managment
- add *Shake To Debug* system, [debug-mode-gyro]
- add support contentURL for DFP
- improve Demo:
    - add pager sample: contains infeed page and a native ad page, https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/PagerViewController.m?at=master&fileviewer=file-view-default
    - improve InfeedViewController: add a native parallax imageView and custom parallax navigationBar
    - improve SwiftViewController: now the sample contains all formats, https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/SwiftViewController.swift?at=master&fileviewer=file-view-default


## Version 2.3.3
#### Release date: December 21th, 2016

 - use new SmartAdServer 6.6 version [libSmartAdServer.a]

## Version 2.3.2
#### Release date: December 19th, 2016

**This version is ATS-compliant, If you push you submit an app after 1th January 2017, you must use this version.**

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

- new template interstitial and square (Appsfire)
- add pod dependency for B4S (If you are using cocoapods, you must remove BeaconForStoreSDK.framework/BeaconForStoreSDK, it will be auto-downloaded by cocoapods)
- use new AdNetworks version:
- use new FBAudienceNetwork 4.18.0 version [FBAudienceNetwork.framework]
- use new DFP 7.16.0 version [GoogleMobileAds.framework]
- use new Flurry 7.8.2 version [libFlurry_7.8.2.a] [libFlurryAds_7.8.2.a]
- use new BeaconForStore 2.0.14 version [BeaconForStoreSDK.framework]

Don't forget to update following libraries :


- [MngAdsSDK]
- [FBAudienceNetwork.framework]
- [GoogleMobileAds.framework]
- [libFlurry_7.8.2.a] [libFlurryAds_7.8.2.a]
- [BeaconForStoreSDK.framework]


## Version 2.3.1
#### Release date: November 11th, 2016

 - core optimization (dispatcher)
 - use new SmartAdServer 6.5 version [libSmartAdServer.a]
 - Remove NSCalendarsUsageDescription permission

Don't forget to update following libraries :


- [MngAdsSDK]
- [libSmartAdServer.a]

## Version 2.3
#### Release date: October 28th, 2016

 - Now MNGADS becomes MADVERTISE MEDIATION and MADVERTISE ADSERVING
 - VAST 2 /VPAID 1 support for MADVERTISE ADSERVING
 - Upgrading MADVERTISE MEDIATION libraries
 - Improve Native Ad assets management with 
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
 - Cache Optimisations
 - Bugs fixes
 - Memory leak fix for banner

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
```


Don't forget to update following libraries :

- [MngAdsSDK]
- [FBAudienceNetwork.framework]
- [libFlurry], [libFlurryAds]
- [libSmartAdServer.a]
- [GoogleMobileAds.framework]

## Version 2.2.1
#### Release date: September 9th, 2016
 -  iOS 10 support, with Limit Ad Tracking changes (in this case we are using vendorId)
 - Now appsfire support videos for square, nativeAds and interstitials
 - Don't forget to update following libraries or use **pod update** :

    - [MngAdsSDK]
    - [FBAudienceNetwork.framework]
    - [AmazonAd.framework] (>= IOS8)
    - [libSmartAdServer.a]

## Version 2.2
#### Release date: August 29th, 2016

 - HTTPS support
 - New appsfire template for banner, medium rectangle and interstitial
 - New Google DFP librairie

Don't forget to update following libraries or use **pod update** :

 - [MngAdsSDK]
 - [GoogleMobileAds.framework]

## Version 2.1.2
#### Release date: July 22th, 2016

no changes, just fix wrong [libSmartAdServer.a] lib on cocoapods.org if pod update has been done on 2016-07-13.

## Version 2.1.1
#### Release date: July 13th, 2016


 - Use lastest smart Adserver and Facebook version
 - Now Amazon available with cocoapods (**If you are using cocoapods, you must remove AmazonAd.framework, it will be auto-downloaded by cocoapods**)
 - Now you can use new predifined sizes 
```objc
extern MNGAdSize const kMNGAdSizeDynamicBanner; //Small Banner Screen width x 50
extern MNGAdSize const kMNGAdSizeDynamicLeaderboard; //Landscape Banner ipad Screen width x 90
```

Don't forget to update following libraries :

 - [MngAdsSDK]
 - [FBAudienceNetwork.framework]
 - [libFlurry], [libFlurryAds]
 - [libSmartAdServer.a]

## Version 2.1
#### Release date: June 21th, 2016

 - Native Ad, add the "AdChoice" badge view for Google/Adx certification in addition to Ad" badge view.
 - Add Smart [In-Feed Ad format] (Parallax or Video)
 - Fixes for smart crashes (ARC
 - Improve mng adserving (interstitial capping, keywords)
 - Improve logging system
 - Add listener for refresh event
 - Remove [LiveRailSDK.framework]
 - Don't forget to update following libraries :
    - [MngAdsSDK]
    - [FBAudienceNetwork.framework]
    - [AmazonAd.framework]
    - [libFlurry], [libFlurryAds]
    - [libSmartAdServer.a](SDK has been converted to ARC for better memory management)

## Version 2.0.8
#### Release date: April 6th, 2016

**You must update [MngAdsSDK] lib and [mnAds Adapters]**

 - bug fixes IOS7 [MngAdsSDK] (after interstitial clicks)
 - upgrade [MngAdsSDK], now appsfire banner allow UIViewAutoresizingFlexibleWidth;


## Version 2.0.7
#### Release date: March 29th, 2016

**You must update [MngAdsSDK] lib and [mnAds Adapters]**

 - bug fixes IOS7 [FBAudienceNetwork.framework], [MngAdsSDK]
 - upgrade [MngAdsSDK], now appsfire banner allow UIViewAutoresizingFlexibleWidth;
 - now mngAds ignores createInterstial 5 secondes after disappear event to avoid overlaping
 - change default_subspec for cocoapods in order to avoid pod update without adapaters (new architecture of v2)

## Version 2.0.6
#### Release date: March 17th, 2016

**You must update [MngAdsSDK] lib and [mnAds Adapters]**

 - upgrade [LiveRailSDK.framework], 
 - bug fixes IOS7 [FBAudienceNetwork.framework], [MngAdsSDK]

## Version 2.0.5
#### Release date: March 13th, 2016

**You must update [MngAdsSDK] lib and [mnAds Adapters]**

 - Optimisation appsfire
 - bug fixes (liverail)

## Version 2.0.4
#### Release date: March 7th, 2016
 - Separate between request and display (see [Interstital implementation])
 - bug fixes

## Version 2.0.3
#### Release date: February 17th, 2016
You need to keep all Ad Network libraries up to date.

 -  Automatic Status bar management (to avoid https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/faq#markdown-header-how-do-i-hide-the-status-bar-on-interstitials-for-sdk-version-203)
 - fix issue for flurry interstitials
 - bug fixes


## Version 2.0.1
#### Release date: February 3th, 2016
You need to keep all Ad Network libraries up to date.

 - Fix compilation errors on simulator

## Version 2.0
#### Release date: January 28th, 2016


 - [libAppsfireSDK.a], [libANSDK] and [libMng-perf.a] libraries have been merged on [MngAdsSDK] SDK for better performance and reduce libraries number
 - We have added [AmazonAd.framework], [LiveRailSDK.framework] , [libFlurryAds_7.3.0.a] to mngads mediation in order to increase fill rate and revenus


## Version 1.5

#### Release date: November 19th, 2015

 - New appsfire SDK that use mngads adserver
 - New DFP version
 - Banner improvement for dynamic height

**You must update [MngAdsSDK], [libAppsfireSDK.a] and [GoogleMobileAds.framework]**


## Version 1.4.3

#### Release date: October 23th, 2015

 - bug fix (EXC_BAD_ACCESS and Facebook)

**You must update [MngAdsSDK]**

## Version 1.4.2

#### Release date: October 16th, 2015

 - use audienceNetwork pod (Facebook)
 - Fixed issue for Appsfire SDK
 - Interstitial improvement, now `isInterstitialShowen` is managed by SDK

**You must update [MngAdsSDK], [libAppsfireSDK.a] and [FBAudienceNetwork.framework]**

## Version 1.4.1

#### Release date: September 18th, 2015


 - IOS9 support (need to disable ATS and disable bitcode (google SDK do not support it) )

>GoogleMobileAdsSdkiOS-7.4.1/GoogleMobileAds.framework/GoogleMobileAds(GADGestureIdUtil.o)' does not contain bitcode. You must rebuild it with bitcode enabled (Xcode setting ENABLE_BITCODE), obtain an updated library from the vendor, or disable bitcode for this target.

**You must update [MngAdsSDK], [libMng-perf.a] , [libSmartAdServer.a] (not available from pod update), [FBAudienceNetwork.framework], [GoogleMobileAds.framework], [libAppsfireSDK.a] and [libANSDK]**

 - **FBAudienceNetwork.framework** and  **libSmartAdServer.a** do not work with **Xcode 6.4**. Therefore, MngAds needs **Xcode 7**.

## Version 1.4

#### Release date: August 25th, 2015


- appNexus can be used download via our Cocoapods
- New SmartAdServer-iOS-SDK-6.0 (dynamicAd, prefetch)
- Add ClickDelegate, The clickDelegate notify you when the ad has been clicked.
- Manage banner size (fixed or responsive) server side
- nativeAd, now we support DFP for premium nativeAd
- Bugs fixing (retain issue, ...)

You must update [MngAdsSDK], [libSmartAdServer.a] (not available from pod update), [FBAudienceNetwork.framework], [GoogleMobileAds.framework] and [libANSDK]

## Version 1.3.9

#### Release date: August 7th, 2015

 - Update Facebook Audience Network library

 - Update [MngAdsSDK] library.

## Version 1.3.8

#### Release date: July 28th, 2015

 - Fix memory issue with smart adapter

 - Update [MngAdsSDK] library.

## Version 1.3.7

#### Release date: July 21th, 2015

  - Update mng perf to 5.1.1 (fix html interstitial issue)

- Update [MngAdsSDK] and [libMng-perf.a] libraries

## Version 1.3.6

#### Release date: July 8th, 2015

  - Manage keywords from mngads console
  - mngperf Adserving improvement (geoloc)

- Update [MngAdsSDK] and [libMng-perf.a] libraries

## Version 1.3.4

#### Release date: June 11th, 2015

 - AdRequest improvement

## Version 1.3.3

#### Release date: June 3th, 2015

 - Manage dynamic size for DFP and appNexus banners
 - Add remote debug mode
 - Add ```@property MNGPriceType priceType;``` and ```@property NSString *localizedPrice;``` on MNGNAtiveObject (use for display "free" icon)
 - Add [Best practice Mngads], optimized use case for several ad formats on one page
 - Update [MngAdsSDK],[libAppsfireSDK.a], [libMng-perf.a] and [GoogleMobileAds.framework] libraries

## Version 1.2.3

#### Release date: May 1st, 2015

 - capping improvement
 - solved smart banner impressions
 - Add guidelines, https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/guidelines

## Version 1.2.2

#### Release date: April 21th, 2015

 - update appsfire SDK to 2.7.1 that use banner in 50pt
 - Improvement of appsfire nativeAd
 - Keywords are now available for all adNeworks with key/value system
 - Added bridge file for swift compatibility

## Version 1.2.1

#### Release date: April 10th, 2015

 - Bug preference.keyword, now allow empty value if location is setted.

## Version 1.2

#### Release date: April 9th, 2015

 - Adding AppNexus adNetwork
 - nativeAd improvements
 - Adding [MNGAdsSDKFactory isInitialized]

## Version 1.1.5

#### Release date: March 31th, 2015

 - Timeout improvement
 - Capping improvement (on placementId and not on MNGAdsFactory)
 - Add keyword preferences
 - Bug fix for non arc projects

## Version 1.1.4

#### Release date: March 18th, 2015

 - Update with latest cocoapods
 - timeout improvements

 - https://bitbucket.org/mngcorp/mngads-demo-ios/commits/tag/v1.1.4
## Version 1.1.3

#### Release date: March 11th, 2015

 - Refreshing of ads is now done by mng ads, improving capping functionality and adding debug more

 - https://bitbucket.org/mngcorp/mngads-demo-ios/commits/tag/v1.1.3

## Version 1.1.2

#### Release date: March 6th, 2015

 - Add support for badge view in native ads (appsfire)

 - https://bitbucket.org/mngcorp/mngads-demo-ios/commits/tag/v1.1.2

## Version 1.1.1

#### Release date: March 5th, 2015

 - Update Google Ads to 7.0.0 + Update FacebookAudienceNetwork to 3.23.1 + Removing Crashlytics

 - https://bitbucket.org/mngcorp/mngads-demo-ios/commits/tag/v1.1.1

## Version 1.1

#### Release date: February 10th, 2015

 - Added ```preferredHeight:(CGFloat)preferredHeight``` to more easily resize banners.


## Version 1.0

#### Release date: December 23th, 2014

 - Initial version

---
[Upgrade Guide]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/upgrading
[MngAdsSDK]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/MNGAds/MNGAds/libMngAds.a?at=master&fileviewer=file-view-default
[libSmartAdServer.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/SmartAdServer-DisplaySDK/SmartAdServer/sdk/?at=master
[FBAudienceNetwork.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/FBAudienceNetwork/?at=master
[GoogleMobileAds.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/Google-Mobile-Ads-SDK/?at=master
[Design Guidelines and Best practices]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/guidelines
[Wiki]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/
[Help Center]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/faq
[AmazonAd.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/AmazonAd.framework/?at=master
[LiveRailSDK.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/LiveRailSDK.framework/?at=master
[libFlurryAds]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/Flurry-iOS-SDK/?at=master
[libFlurry]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/Flurry-iOS-SDK/?at=master
[Interstital implementation]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Home#markdown-header-interstitial
[mnAds Adapters]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/MNGAds/MNGAds/?at=master
[In-Feed Ad format]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Home#markdown-header-infeed
[App Transport Security]:https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW60
[debug-mode-gyro]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/debug-mode-gyro
[BeaconForStoreSDK.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/d41507a6c8eac3829efd9b05247acac1fcc51f8f/Demo/MNG-Ads-SDK/BeaconForStoreSDK.framework/?at=master
[umoove.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Umoove.framework/?at=master