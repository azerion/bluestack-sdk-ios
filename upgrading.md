# upgrading SDK
## Upgrading to 2.3
### New features
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
```


Don't forget to update following librairies :

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
Librairies

**If you are using cocoapods, you must remove AmazonAd.framework, it will be auto-downloaded by cocoapods**

Don't forget to update following librairies :

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

### Librairies

 - The following librairies are not required anymore for the sdk

     - Remove [LiveRailSDK.framework]


 - Don't forget to update following librairies :
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



[MngAdsSDK]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/MNGAds/?at=master
[libSmartAdServer.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/SmartAdServer-DisplaySDK/SmartAdServer/sdk/?at=master
[FBAudienceNetwork.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/FBAudienceNetwork/?at=master
[GoogleMobileAds.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/Google-Mobile-Ads-SDK/GoogleMobileAdsSdkiOS-7.6.0/?at=master
[Design Guidelines and Best practices]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/guidelines
[Wiki]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/
[Help Center]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/faq
[AmazonAd.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/AmazonAd.framework/?at=master
[LiveRailSDK.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/LiveRailSDK.framework/?at=master
[libFlurryAds]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/Flurry-iOS-SDK/?at=master
[libFlurry]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/Flurry-iOS-SDK/?at=master
[libMNGAdsDFPAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/MNGAds/libMNGAdsDFPAdapter.a?at=master&fileviewer=file-view-default
[libMNGAdsFacebookAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/MNGAds/libMNGAdsFacebookAdapter.a?at=master&fileviewer=file-view-default
[libMNGAdsSASAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/MNGAds/libMNGAdsSASAdapter.a?at=master&fileviewer=file-view-default
[libMNGAmazonAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/MNGAds/libMNGAmazonAdapter.a?at=master&fileviewer=file-view-default
[libMNGFlurryAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/MNGAds/libMNGFlurryAdapter.a?at=master&fileviewer=file-view-default
[libMNGLiveRailAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/MNGAds/libMNGLiveRailAdapter.a?at=master&fileviewer=file-view-default
[Using CocoaPods]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Using%20CocoaPods
[In-Feed Ad format]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Home#markdown-header-infeed

