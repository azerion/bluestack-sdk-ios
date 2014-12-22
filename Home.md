# MngAds for IOS

MNG Ads provides functionalities for monetizing your mobile application: from premium sales with reach media, video and innovative formats, it facilitates inserting native mobile ads as well all standard display formats. MngAds SDK is a library that allow you to handle the following Ads servers with the easy way

It contains a dispacher that will select an ads server according to the priority and state.

## Version
1.0

## Manual Install

- download [MngAdsSDK.zip]
- unzip [MngAdsSDK.zip]
- drag and drop it in your project
- check that libMngAds.a existe in "Link Binary With Libraries"


MngAds SDK needs:

- libSmartAdServer.a
- FBAudienceNetwork.framework
- GoogleMobileAdsSdkiOS-6.12.2
- CoreGraphics.framework
- QuartzCore.framework
- SystemConfiguration.framework
- MediaPlayer.framework
- CoreMotion.framework
- EventKitUI.framework
- EventKit.framework
- AdSupport.framework
- StoreKit.framework
- CoreLocation.framework

## Sample Application

Included is a [MngAds sample app] to use as example and for help on MngAds integration. This basic application allows users to test our different format.

## Start Integrating

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
#### Timeout
The time given to the ad view to download the ad data. After this time, the dispacher stops the ad server running (with failure) and move to the next.

the default timeout is 1s.
```objc
adsFactory = [[MNGAdsSDKFactory alloc]init];
adsFactory.timeout = 3;
```
#### isBusy
Before making a request you have to check that factory not busy (handling old request).

Ads factory is busy means that it has not finished the previous request yet.

isBusy will be setted to true when factory start handling request.

isBusy will be setted to false when factory finish handling request.
##### example:
```objc
if (bannerAdsFactory.isBusy) {
NSLog(@"Ads Factory is busy");
}else{
NSLog(@"Ads Factory is not busy");
}
[bannerAdsFactory createBannerInFrame:CGRectMake(0, 0, 320, 50)]
if (bannerAdsFactory.isBusy) {
NSLog(@"Ads Factory is busy");
}else{
NSLog(@"Ads Factory is not busy");
}
```
######Log:
```shell
$Ads Factory is not busy
$Ads Factory is busy
```
### Banner
#####Init factory

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
#####Make a request
To make a request you have to call 'createBannerInFrame'. this method return a bool value (canHandleRequest) 

```objc
if([bannerAdsFactory createBannerInFrame:CGRectMake(0, 0, 320, 50)]){
//Wait callBack from delegate
}else{
//adsFactory can not handle your request
}
```

#####Handle callBack from BannerDelegate
adsAdapter:bannerDidLoad: will be called by the SDK when your bannerView is ready. now you can add your bannerView to th ViewHierarchy.
```objc
-(void)adsAdapter:(MNGAdsAdapter *)adsAdapter bannerDidLoad:(UIView *)bannerView{
NSLog(@"adsAdapterBannerDidLoad:");
_bannerView = bannerView;
_bannerView.frame = CGRectMake(0, 20, 320, 50);
[self.view addSubview:_bannerView];
}
```

adsAdapter:bannerDidFailWithError: will be called when all ads servers fail. it will return the error of last called ads server.
```objc
-(void)adsAdapter:(MNGAdsAdapter *)adsAdapter bannerDidFailWithError:(NSError *)error{
NSLog(@"%@",error);
}
```

### Interstitial
#####Init factory

To create a interstitial you have to init an object with type MNGAdsSDKFactory and set the interstitalDelegate and the viewController.

```objc
interstitialAdsFactory = [[MNGAdsSDKFactory alloc]init];
interstitialAdsFactory.interstitialDelegate = self;
interstitialAdsFactory.viewController = self;
```
You have also to set placementId (minimum one time)

```objc
interstitialAdsFactory.placementId = @"/YOUR_APP_ID/PLACEMENT_ID";
```
#####Make a request
To make a request you have to call 'createInterstitial'. this method return a bool value (canHandleRequest) 

```objc
if([interstitialAdsFactory createInterstitial]){
//Wait callBack from delegate
}else{
//adsFactory can not handle your request
}
```

#####Handle callBack from InterstitialDelegate
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

### Native Ads
Native ads give you the control to design the perfect ad units for your app. With our Native Ad API, you can determine the look and feel, size and location of your ads. Because you decide how the ads are formatted, ads can fit seamlessly in your application.
#####Init factory

To create a nativeAd  you have to init an object with type MNGAdsSDKFactory and set the nativeDelegate.

```objc
nativeAdsFactory = [[MNGAdsSDKFactory alloc]init];
nativeAdsFactory.nativeDelegate = self;
```
You have also to set placementId (minimum one time)

```objc
nativeAdsFactory.placementId = @"/YOUR_APP_ID/PLACEMENT_ID";
```
#####Make a request
To make a request you have to call 'createNative'. this method return a bool value (canHandleRequest) 

```objc
if([nativeAdsFactory createNative]){
//Wait callBack from delegate
}else{
//adsFactory can not handle your request
}
```

#####Handle callBack from NativeDelegate
adsAdapter:nativeObjectDidLoad: will be called by the SDK when your nativeObject is ready. now you can create your own view.
```objc
-(void)adsAdapter:(MNGAdsAdapter *)adsAdapter nativeObjectDidLoad:(MNGNAtiveObject *)nativeObject{
NSLog(@"adsAdapterNativeObjectDidLoad:");
self.titleLabel.text = nativeObject.title;
self.contextLabel.text = nativeObject.socialContext;
self.bodyLabel.text = nativeObject.body;
...
}
```

adsAdapter:nativeObjectDidFailWithError: will be called when all ads servers fail. it will return the error of last called ads server.
```objc
-(void)adsAdapter:(MNGAdsAdapter *)adsAdapter nativeObjectDidFailWithError:(NSError *)error{
NSLog(@"%@",error);
}
```
#### Preferences Object
Preferences object is an optional parameter that allow you select ads by user info.
informations that you can set are:

- age : age of user
- location : geographical position of the user. *Important:* your application can be rejected by Apple if you use the device's location *only* for advertising.
- language : language of user (ISO code)
- gender : gender of user

```objc
#import "MNGPreference.h"
...
MNGPreference * preference = [[MNGPreference alloc]init];
preference.age = 25;
preference.language = @"fr";
preference.gender = MNGGenderFemale;
preference.location = [[CLLocation alloc]initWithLatitude:48.876 longitude:10.453];
[bannerAdsFactory createBannerInFrame:CGRectMake(0, 0, 320, 50)withPreferences:preference];
```
`Note`: this [link] can help you to get device location.

----

[link]:http://www.tutorialspoint.com/ios/ios_location_handling.htm
[Smart ads server]:http://help.smartadserver.com/fr/Default.htm#../../../../specifications/Content/MobileSpecifications/Apps.htm
[Mng-perf]:https://dashboard.mng-ads.com/sdk/mng-perf-sdk-integration-ios.html
[Google DFP]:https://developers.google.com/mobile-ads-sdk/download#download
[Facebook Audience Network]:https://developers.facebook.com/docs/ios?locale=fr_FR
[MngAdsSDK.zip]:http://dispatcher.mng-ads.com/sdk/ios/MngAdsSDK.zip
 [MngAds sample app]:https://bitbucket.org/mngcorp/mngads-demo-ios/src