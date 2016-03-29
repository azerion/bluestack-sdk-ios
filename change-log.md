## Change log and release notes for the MngAds SDK for iOS.

See [Wiki], [Design Guidelines and Best practices] and [Help Center]  for more detailed informations

## Version 2.0.7
#### Release date: March 29th, 2016

**You must update [MngAdsSDK] lib and [mnAds Adapters]**

 - upgrade [MngAdsSDK], now appsfire banner allow UIViewAutoresizingFlexibleWidth;, 
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
You need to keep all Ad Network librairies up to date.

 -  Automatic Status bar management (to avoid https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/faq#markdown-header-how-do-i-hide-the-status-bar-on-interstitials-for-sdk-version-203)
 - fix issue for flurry interstitials
 - bug fixes


## Version 2.0.1
#### Release date: February 3th, 2016
You need to keep all Ad Network librairies up to date.

 - Fix compilation errors on simulator

## Version 2.0
#### Release date: January 28th, 2016

you mus check [Upgrade Guide]. You need to keep all Ad Network librairies up to date.

 - [libAppsfireSDK.a], [libANSDK] and [libMng-perf.a] libraries have been merged on [MngAdsSDK] SDK for better performance and reduce librairies number
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

**You must check [Upgrade Guide].**

 - IOS9 support (need to disable ATS and disable bitcode (google SDK do not support it) )

>GoogleMobileAdsSdkiOS-7.4.1/GoogleMobileAds.framework/GoogleMobileAds(GADGestureIdUtil.o)' does not contain bitcode. You must rebuild it with bitcode enabled (Xcode setting ENABLE_BITCODE), obtain an updated library from the vendor, or disable bitcode for this target.

**You must update [MngAdsSDK], [libMng-perf.a] , [libSmartAdServer.a] (not available from pod update), [FBAudienceNetwork.framework], [GoogleMobileAds.framework], [libAppsfireSDK.a] and [libANSDK]**

 - **FBAudienceNetwork.framework** and  **libSmartAdServer.a** do not work with **Xcode 6.4**. Therefore, MngAds needs **Xcode 7**.

## Version 1.4

#### Release date: August 25th, 2015

You must check [Upgrade Guide].

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

- Update [MngAdsSDK] and [libMng-perf.a] librairies

## Version 1.3.6

#### Release date: July 8th, 2015

  - Manage keywords from mngads console
  - mngperf Adserving improvement (geoloc)

- Update [MngAdsSDK] and [libMng-perf.a] librairies

## Version 1.3.4

#### Release date: June 11th, 2015

 - AdRequest improvement

## Version 1.3.3

You must check [Upgrade Guide].
#### Release date: June 3th, 2015

 - Manage dynamic size for DFP and appNexus banners
 - Add remote debug mode
 - Add ```@property MNGPriceType priceType;``` and ```@property NSString *localizedPrice;``` on MNGNAtiveObject (use for display "free" icon)
 - Add [Best practice Mngads], optimized use case for several ad formats on one page
 - Update [MngAdsSDK],[libAppsfireSDK.a], [libMng-perf.a] and [GoogleMobileAds.framework] librairies

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
[libSmartAdServer.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/sdk/libSmartAdServer.a?at=master
[FBAudienceNetwork.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/FBAudienceNetwork/?at=master
[GoogleMobileAds.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/Google-Mobile-Ads-SDK/GoogleMobileAdsSdkiOS-7.6.0/?at=master
[Design Guidelines and Best practices]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/guidelines
[Wiki]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/
[Help Center]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/faq
[AmazonAd.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/AmazonAd.framework/?at=master
[LiveRailSDK.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/LiveRailSDK.framework/?at=master
[libFlurryAds_7.3.0.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/Flurry-iOS-SDK/?at=master
[libFlurry_7.3.0.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/Flurry-iOS-SDK/?at=master
[Interstital implementation]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Home#markdown-header-interstitial
[mnAds Adapters]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/MNGAds/MNGAds/?at=master
