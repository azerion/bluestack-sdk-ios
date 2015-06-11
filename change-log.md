## Change log and release notes for the MngAds SDK for iOS.
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

#### Release date: Febuary 10th, 2015

 - Added ```preferredHeight:(CGFloat)preferredHeight``` to more easily resize banners.


## Version 1.0

#### Release date: December 23th, 2014

 - Initial version

---
[Upgrade Guide]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/upgrading
[GoogleMobileAds.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/Google-Mobile-Ads-SDK/GoogleMobileAdsSdkiOS-7.0.0/?at=master
[libAppsfireSDK.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/AppsfireSDK/?at=master
[libMng-perf.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/Mng-perf/?at=master
[Best practice Mngads]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/guidelines
[MngAdsSDK]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/MNGAds/?at=master

