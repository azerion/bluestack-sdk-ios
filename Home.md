![mad_AdNetworkMediation_rgb_small.png](https://bitbucket.org/repo/GyRXRR/images/3981639300-mad_AdNetworkMediation_rgb_small.png) for IOS

[TOC]

MNG Ads provides functionalities for monetizing your mobile application: from premium sales with reach media, video and innovative formats, it facilitates inserting native mobile ads as well all standard display formats. MngAds SDK is a library that allow you to handle the following Ads servers with the easy way :

- [Smart ads server]
- [Facebook Audience Network]
- [MNG Ad Server] (Mng + AppsFire)
- [Google DFP]
- [AppNexus] (Via Server)
- [Amazon]
- [Flurry]
- [Beacon For Store]

It contains a dispacher that will select an ads server according to the priority and state ([mngAds state diagram]).

## Requirements

Requires **Xcode 8**.
Requires **git lfs**.

- First Download and install the [git-lfs command line client](https://git-lfs.github.com)
- Then install the Git LFS filters:
```
#!unix

$ git lfs install —force
```
For more about installing git LFS go to:
https://git-lfs.github.com

## Version
See [Change Log] and [Upgrade Guide].

## Guidelines

See [Design Guidelines and Best practices]

## Help and Troubleshooting

[Help Center]
Answers to frequently asked questions


## Using CocoaPods

The MngAds SDK is available through Cocoapods. see [Using CocoaPods] section.


## Manual Install

- download [MngAdsSDK] from our demo project, **you must use version of  Ads servers's librairies in used on demo project.**
- drag and drop it in your project
- check that libMngAds.a exist in "Link Binary With Libraries"

- For manual installation without pod, do not forget to include the "-ObjC" linker flag in "Other Linker Flags" under "Build Settings" in the project file." [see our Faq]


MngAds SDK needs, these libraries are in demo project :

- [libSmartAdServer.a], use version >=6.3, in used on demo project.
- [FBAudienceNetwork.framework]
- [GoogleMobileAds.framework], use version >=7.8.1, in used on demo project.
- [AmazonAd.framework]
- [libFlurryAds.a]
- [libFlurry.a]
- [BeaconForStoreSDK.framework] (use geographical position of the user)
- [BeaconForStoreStorage.bundle] (use geographical position of the user)
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
 - [libMAdvertiseB4SAdapter.a] (use geographical position of the user)

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

## Sample Application

Included is a [MngAds sample app] to use as example and for help on MngAds integration. This basic application allows users to test our differents formats.

## Start Integrating

### Enable Debug Mode

To enable debug mode you have to use class method **setDebugModeEnabled** :

```
 [MNGAdsSDKFactory setDebugModeEnabled:Yes];
```
Can you please remove debug mode on production.

### Initializing the SDK

You have to init the SDK in AppDelegate.m in application:didFinishLaunchingWithOptions:
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
```
### MAdvertiseBeacon

- Get Ebeacon technology to propose to the advertisers to target the users inside the point of sale. 
- An installation base of 12,500 ebeacons ready to track the users.
- An exclusive format in Push notification to the users inside a tabacco shop, press shop, pharmay or mall.

### Initializing Beacons
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
### Banner
##### Init factory

To create a banner you have to init an object with type MNGAdsSDKFactory and set the bannerDelegate and the viewController.

```objc
bannerAdsFactory = [[MNGAdsSDKFactory alloc]init];
bannerAdsFactory.bannerDelegate = self;
bannerAdsFactory.viewController = self;
```
You have also to set placementId (minimum one time)

```objc
bannerAdsFactory.placementId = @"/YOUR_APP_ID/PLACEMENT_ID";
```
##### Make a request
To make a request you have to call 'loadBannerInFrame'.

```objc
[bannerAdsFactory loadBannerInFrame:kMNGAdSizeDynamicBanner]
```

##### Handle callBack from BannerDelegate
adsAdapter:bannerDidLoad: will be called by the SDK when your bannerView is ready. now you can add your bannerView to th ViewHierarchy.
```objc
-(void)adsAdapter:(MNGAdsAdapter  *)adsAdapter bannerDidLoad:(UIView  *)bannerView preferredHeight:(CGFloat)preferredHeight{
    NSLog(@"adsAdapterBannerDidLoad:");
    _bannerView = bannerView;
    _bannerView.frame = CGRectMake(0, 20, 320, preferredHeight);
    [self.view addSubview:_bannerView];
}
```

adsAdapter:bannerDidFailWithError: will be called when all ads servers fail. it will return the error of last called ads server.
```objc
-(void)adsAdapter:(MNGAdsAdapter *)adsAdapter bannerDidFailWithError:(NSError *)error{
NSLog(@"%@",error);
}
```
Some Ad Network (like Smart ads server) allow user to expand and collapse ad.

Even on refresh, banner can change the size.

adsAdapter:bannerDidChangeFrame: will be called when ad did change size
```objc
-(void)adsAdapter:(MNGAdsAdapter *)adsAdapter bannerDidChangeFrame:(CGRect)frame{
    ...
}
```

##### Handle callBack from RefreshDelegate
If you want tobe notified on refresh, you have to set refresh delegate
```objc
bannerAdsFactory.refreshDelegate = self;
```
On banner refresh, the SDK invoke the calback
```objc
-(void)adsAdapterBannerDidRefresh:(MNGAdsAdapter *)adsAdapter{
    ...
}
```

On banner fail to refresh, the SDK invoke the calback
```objc
-(void)adsAdapterBannerDidRefresh:(MNGAdsAdapter *)adsAdapter{
    ...
}
```

### MNGAdSize
Mng ads provides variant pre-defined sizes ( example below).
```objc
/**
 MNGAdSize the same of CGRect
 */
typedef CGRect MNGAdSize;

extern MNGAdSize const kMNGAdSizeBanner; //Small Banner 320 x 50
extern MNGAdSize const kMNGAdSizeDynamicBanner; //Small Banner Screen width x 50
extern MNGAdSize const kMNGAdSizeLargeBanner; //Large Banner 320 x 100
extern MNGAdSize const kMNGAdSizeFullBanner; //Full Banner ipad 468 x 60
extern MNGAdSize const kMNGAdSizeLeaderboard; //Landscape Banner ipad 728 x 90
extern MNGAdSize const kMNGAdSizeDynamicLeaderboard; //Landscape Banner ipad Screen width x 90
extern MNGAdSize const kMNGAdSizeMediumRectangle; //Square Banner 300 x 250
```
Example:

```objc
    MNGAdSize size;
    if (isSquare) {
        size = kMNGAdSizeMediumRectangle;
    }else{
        BOOL isIPAD = ([[UIDevice currentDevice] userInterfaceIdiom] == UIUserInterfaceIdiomPad);
        size = (isIPAD)?kMNGAdSizeDynamicLeaderboard:kMNGAdSizeDynamicBanner;
    }
    [bannerAdsFactory loadBannerInFrame:size];
```

### Infeed
##### Init factory

To create an **In-Feed** Ad format ( the ads that show up in the middle of the stream as you scroll through your content), you must init an object with type MNGAdsSDKFactory and set the infeedDelegate and the viewController.

```objc
infeedAdsFactory = [[MNGAdsSDKFactory alloc]init];
infeedAdsFactory.infeedDelegate = self;
infeedAdsFactory.viewController = self;
```
You have also to set placementId (minimum one time)

```objc
infeedAdsFactory.placementId = @"/YOUR_APP_ID/PLACEMENT_ID";
```
##### Make a request
To make a request you have to call 'loadInfeedInFrame'.

```objc
[infeedAdsFactory loadInfeedInFrame:CGRectMake(0, 0, 320, 50)]
```

##### Handle callBack from InfeedDelegate
adsAdapter:infeedDidLoad: will be called by the SDK when your bannerView is ready. now you can add your bannerView to th ViewHierarchy.
```objc
-(void)adsAdapter:(MNGAdsAdapter  *)adsAdapter infeedDidLoad:(UIView  *)bannerView{
    NSLog(@"adsAdapterInfeedDidLoad:");
    [self.view addSubview:_bannerView];
}
```

`NB:` infeed does not return preferredHeight like banner because infeed height depends of width so you can use one the standard ration:

- 5:3 (called also 15:9) : the one used in our demo
- 16:9 : is the international standard format of HDTV

```objc
- (CGFloat)tableView:(UITableView *)tableView heightForRowAtIndexPath:(NSIndexPath *)indexPath{
    if (indexPath.row == INFEED_ROW) {
        if (_infeedView) {
            return self.view.frame.size.width * (3./5.);
        }
        return 0;
    }else{
        return OTHER_CELL_ROW_HEIGHT;
    }
}
```

adsAdapter:infeedDidFailWithError: will be called when all ads servers fail. it will return the error of last called ads server.

```objc
-(void)adsAdapter:(MNGAdsAdapter *)adsAdapter infeedDidFailWithError:(NSError *)error{
NSLog(@"%@",error);
}
```
##### Handle callBack from RefreshDelegate
If you want tobe notified on refresh, you have to set refresh delegate (same as banner)
```objc
infeedAdsFactory.refreshDelegate = self;
```

### Interstitial

**On info.plist if you are using "View controller-based status bar appearance" (UIViewControllerBasedStatusBarAppearance), it must be setted to YES**


![statusbar.png](https://bitbucket.org/repo/aen579/images/4293410302-statusbar.png)


##### Init factory

To create an interstitial you must init an object with type MNGAdsSDKFactory and set the interstitalDelegate and the viewController.

```objc
interstitialAdsFactory = [[MNGAdsSDKFactory alloc]init];
interstitialAdsFactory.interstitialDelegate = self;
interstitialAdsFactory.viewController = self;
```
You have also to set placementId (minimum one time)

```objc
interstitialAdsFactory.placementId = @"/YOUR_APP_ID/PLACEMENT_ID";
```
##### Make a request
To make a request you must call 'loadInterstitial'. 

```objc
[interstitialAdsFactory loadInterstitial];
```

##### Handle callBack from InterstitialDelegate
adsAdapterInterstitialDidLoad: will be called by the SDK when your Interstitial is ready. Interstitial will be showen.
```objc
-(void)adsAdapterInterstitialDidLoad:(MNGAdsAdapter *)adsAdapter{
NSLog(@"adsAdapterInterstitialDidLoad");
...
}
```

adsAdapter:interstitialDidFailWithError: will be called when all ads servers fail. it will return the error of last called ads server.
```objc
-(void)adsAdapter:(MNGAdsAdapter *)adsAdapter interstitialDidFailWithError:(NSError *)error{
NSLog(@"%@",error);
}
```
adsAdapterInterstitialDisappear: will be called when intertisialView did disappear. now you can update your UI for example.
```objc
-(void)adsAdapterInterstitialDisappear:(MNGAdsAdapter *)adsAdapter{
NSLog(@"adsAdapterInterstitialDisappear");
//For example
HomeViewController *home =  [[HomeViewController alloc]init];
[self.navigationController pushViewController:home animated:YES];
}
```

##### Disable auto-displaying 
With v2.0.4 you can disable auto-displaying.

```objc
[interstitialAdsFactory loadInterstitialWithPreferences:preferences autoDisplayed:NO];
```
To show the interstitial after succes you have call [displayInterstitial].

To check if the interstitial is reday to be showen, you have to call [isInterstitialReady].

```objc
if ([interstitialAdsFactory isInterstitialReady]) {
    [interstitialAdsFactory displayInterstitial];
}
```

___info:___ To test auto-displayin disabled on demo, you have to go to the page interstitial. others interstitials (return background, when change from page to page...) are with auto-displaying.

### Native Ads
Native ads give you the control to design the perfect ad units for your app. With our Native Ad API, you can determine the look and feel, size and location of your ads. Because you decide how the ads are formatted, ads can fit seamlessly in your application.
##### Init factory

To create a nativeAd  you have to init an object with type MNGAdsSDKFactory and set the nativeDelegate.

```objc
nativeAdsFactory = [[MNGAdsSDKFactory alloc]init];
nativeAdsFactory.nativeDelegate = self;
```
You have also to set placementId (minimum one time)

```objc
nativeAdsFactory.placementId = @"/YOUR_APP_ID/PLACEMENT_ID";
```
##### Make a request
To make a request you have to call 'loadNative'. 

```objc
[nativeAdsFactory loadNative]
```

##### Handle callBack from NativeDelegate
adsAdapter:nativeObjectDidLoad: will be called by the SDK when your nativeObject is ready. now you can create your own view.
```objc
-(void)adsAdapter:(MNGAdsAdapter *)adsAdapter nativeObjectDidLoad:(MNGNAtiveObject *)nativeObject{
NSLog(@"adsAdapterNativeObjectDidLoad:");
self.titleLabel.text = nativeObject.title;
self.contextLabel.text = nativeObject.socialContext;
self.bodyLabel.text = nativeObject.body;
//possibility to customize the badge title
[nativeObject updateBadgeTitle:@"Publicité"]; 
badgeView = nativeObject.badgeView;
[nativeObject setMediaContainer:self.container];
...
}
```

adsAdapter:nativeObjectDidFailWithError: will be called when all ads servers fail. it will return the error of last called ads server.
```objc
-(void)adsAdapter:(MNGAdsAdapter *)adsAdapter nativeObjectDidFailWithError:(NSError *)error{
NSLog(@"%@",error);
}
```

See [Native Ads guidelines]

### ClickDelegate
The clickDelegate notify you when the ad has been clicked.

```objc
//.h
@interface ViewController : UIViewController<MNGClickDelegate>

//.m
adsFactory.clickDelegate = self;

...

-(void)adsAdapterAdWasClicked:(MNGAdsAdapter *)adsAdapter{
    NSLog(@"Ad Clicked");
    ...
}
```

If you show an interstitial at the didEnterForeground, you can use click delegate to check up if the application enter background by user or after an ad click.

```objc
- (void)applicationDidEnterBackground:(UIApplication *)application {
    if ([self.lastClickDate timeIntervalSinceNow] >= -10.) {
        _isAdClicked = YES;
        NSLog(@"Next enter background will be ignored");
    }
    
}

- (void)applicationDidBecomeActive:(UIApplication *)application {
    if ([MNGAdsSDKFactory isInitialized] && !_isAdClicked) {
        NSLog(@"applicationDidBecomeActive");
        [self displayInters];
    }
    _isAdClicked = NO;
}

-(void)adsAdapterAdWasClicked:(MNGAdsAdapter *)adsAdapter{
    NSLog(@"Banner clicked");
    [((AppDelegate*)[[UIApplication sharedApplication]delegate])setLastClickDate:[NSDate date]];
}

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
available v2.5
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
- Calling releaseMemory at the dealloc of delegate
```objc
    -(void)dealloc{
        [intersFactory releaseMemory];
        intersFactory = nil;
    }
```
----

[ARC]:https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/AutomaticReferenceCounting.html
[link]:http://www.tutorialspoint.com/ios/ios_location_handling.htm
[Smart ads server]:http://help.smartadserver.com/fr/Default.htm#../../../../specifications/Content/MobileSpecifications/Apps.htm
[Mng-perf]:https://bitbucket.org/mngcorp/mngperf-demo-ios
[Google DFP]:https://developers.google.com/mobile-ads-sdk/download#download
[Facebook Audience Network]:https://developers.facebook.com/docs/ios?locale=fr_FR
[MngAdsSDK]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/MNGAds/MNGAds/libMngAds.a?at=master&fileviewer=file-view-default
[MngAds sample app]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD?at=master
[appsfire]:https://github.com/appsfire/Appsfire-iOS-SDK
[Help Center]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/faq
[Change Log]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/change-log
[Upgrade Guide]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/upgrading
[AppNexus]:http://www.appnexus.com/fr
[libANSDK]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/AppNexusSDK/?at=master

[libSmartAdServer.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/SmartAdServer-DisplaySDK/SmartAdServer/sdk/?at=master
[FBAudienceNetwork.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/FBAudienceNetwork/?at=master
[GoogleMobileAds.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/Google-Mobile-Ads-SDK/?at=master
[libAppsfireSDK.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/AppsfireSDK/?at=master
[libMng-perf.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/Mng-perf/?at=master
[Using CocoaPods]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Using%20CocoaPods
[mngAds state diagram]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/diagram
[Installation guide for Swift]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Swift
[Design Guidelines and Best practices]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/guidelines
[MNG Ad Server]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/MNGAds/MNGAds/?at=master

[AmazonAd.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/AmazonAd.framework/?at=master
[LiveRailSDK.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/LiveRailSDK.framework/?at=master
[libFlurryAds.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/Flurry-iOS-SDK/?at=master
[libFlurry.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/Flurry-iOS-SDK/?at=master
[Native Ads guidelines]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/nativead
[libMNGAdsDFPAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/MNGAds/libMNGAdsDFPAdapter.a?at=master&fileviewer=file-view-default
[libMNGAdsFacebookAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/MNGAds/libMNGAdsFacebookAdapter.a?at=master&fileviewer=file-view-default
[libMNGAdsSASAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/MNGAds/libMNGAdsSASAdapter.a?at=master&fileviewer=file-view-default
[libMNGAmazonAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/MNGAds/libMNGAmazonAdapter.a?at=master&fileviewer=file-view-default
[libMNGFlurryAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/MNGAds/libMNGFlurryAdapter.a?at=master&fileviewer=file-view-default
[libMNGLiveRailAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/MNGAds/libMNGLiveRailAdapter.a?at=master&fileviewer=file-view-default
[see our Faq]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/faq#markdown-header--objc-linker-flag-required

[libMAdvertiseB4SAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/MNGAds/libMAdvertiseB4SAdapter.a?at=master&fileviewer=file-view-default
[BeaconForStoreSDK.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/d41507a6c8eac3829efd9b05247acac1fcc51f8f/Demo/MNG-Ads-SDK/BeaconForStoreSDK.framework/?at=master
[BeaconForStoreStorage.bundle]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/BeaconForStoreStorage.bundle/?at=master

[App Transport Security]:https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW60
[extended the ATS deadline]:https://developer.apple.com/news/?id=12212016b&1482372961