![MNG-Ads-1.png](https://bitbucket.org/repo/aen579/images/3739691856-MNG-Ads-1.png) iOS for
![4193248577-af.png](https://bitbucket.org/repo/aen579/images/2031262448-4193248577-af.png) only


[TOC]

# Introduction

MNG Ads can be used for appsfire nativeAds only.

 - http://appsfire.com/

The Monetization features of Appsfire SDK allows you to display ads in your application:

 
 - Interstitial ads, A full-screen native ad unit for iPhone & iPad, we call it the [Sushi].
 - An in-stream native ad unit which allows you to deeply integrate our ads in your application's design, we call it [Sashimi]. 

## Using CocoaPods

The MngAds SDK is available through [Cocoapods], a popular dependency management system for Objective-C projects.

To download and incorporate the MngAds SDK into your project using Cocoapods, add the following line to your project's podfile:

```ruby
pod "MNGAds" 
```

## Manual Install

- download [MNGAds SDK for appsfire] from our demo project, **you must use version of  Ads servers's librairies in used on demo project.**
- drag and drop it in your project
- check that libMngAds.a exist in "Link Binary With Libraries"


MngAds SDK needs, these libraries are in demo project :


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
- Accelerate/Accelerate.h Framework
- CoreMedia
## Start Integrating appsfire

### Banner

```
...
#import "MNGHimonoBannerView"
...
MNGHimonoBannerView *himonoView;
...

// init banner view
himonoView = [[MNGHimonoBannerView alloc] initWithFrame:CGRectMake(0, 0, SCREEN_WIDTH, 50)];
himonoView.delegate = self;
himonoView.refreshAutomatically = YES;
himonoView.refreshInterval = 30;
self.bannerHeightConstraint.constant = himonoView.frame.size.height;
self.bannerWidthConstraint.constant = himonoView.frame.size.width;
[self.container addSubview:himonoView];
    
```
##### Ad size MNGAdSize
```
extern CGSize const kMNGAdServerSizeBanner50; //Small Banner screenWidth x 50
extern CGSize const kMNGAdServerSizeLargeBanner100; //Large Banner screenWidth x 100
extern CGSize const kMNGAdServerSizeFullBanner60; //Full Banner ipad screenWidth x 60
extern CGSize const kMNGAdServerSizeLeaderboard90; //Landscape Banner ipad screenWidth x 90
extern CGSize const kMNGAdServerSizeMediumRectangle; //Square Banner 300 x 250

```

##### Make a request
To make a request you must call loadAd

```
[himonoView loadAd:@"YOUR_PUBLISHER_ID"];
```

##### Handle callBack from MNGHimonoBannerViewDelegate
```objc
- (void)himonoBannerViewDidLoadAd:(MNGHimonoBannerView *)himonoBannerView {
    NSLog(@"bannerView did load");
    [self.container addSubview:bannerView];
}

- (void)himonoBannerViewDidFailToLoadAd:(MNGHimonoBannerView *)himonoBannerView withError:(NSError *)error {
    NSLog (@"himonoBannerViewDidFailToLoadAd");
}

- (void)himonoBannerViewDidRecordClick:(MNGHimonoBannerView *)himonoBannerView {
    NSLog (@"himonoBannerViewDidRecordClick");
}
```

### Interstitial

```objc
    ...
#import "MNGDisplayableNativeAd.h"
#import "MNGSushiViewController.h"
...
MNGDisplayableNativeAd *interNativeAd;
MNGSushiViewController *interViewController;

// init interstitial
interNativeAd = [[MNGDisplayableNativeAd alloc] init];
interNativeAd.publisherId = @"YOUR_PUBLISHER_ID";
interNativeAd.delegate = self;
    
```
##### Make a request 
To make a request you have to call loadAd 

```
[interNativeAd loadAd];
```
##### Handle callBack from MNGNativeAdDelegate
```objc
-(void)nativeAdDidLoad:(MNGNativeAd *)nativeAd {
    NSLog(@"intertitial did load");
}

-(void)nativeAd:(MNGNativeAd *)nativeAd didFailWithError:(NSError *)error {
    NSLog(@"intertitial did fail with error : %@",error);
    
}
-(void)intertitialWillDisappear:(nonnull MNGInterstitialViewController *)interstitialViewController{
    NSLog(@"intertitial will disappear");
}

-(void)intertitialDidClicked:(MNGInterstitialViewController *)interstitialViewController{
    NSLog(@"intertitial did clicked");
}
```

##### Displaying interstitial
```objc
if (interNativeAd != nil) {
    interViewController = [interNativeAd getSushiViewController];
    interViewController.viewController = myViewController;  // Present from your view controller
    interViewController.delegate = self;
    [interViewController present];
}
```

##### Handle callBack from MNGSushiViewDelegate
```objc
-(void)interstitialDidAppear:(nonnull MNGSushiViewController *)sushiViewController {
    NSLog (@"interstitialDidAppear");
}

-(void)interstitialWasClicked:(nonnull MNGSushiViewController *)sushiViewController {
    NSLog (@"interstitialWasClicked");
}

-(void)interstitialWillDisappear:(nonnull MNGSushiViewController *)sushiViewController {
    NSLog (@"interstitialWillDisappear");
}
```
### Getting native ads metadata

```objc
...
#import "MNGNativeAd.h"
...
MNGNativeAd *nativeAd;

// init nativeAd
nativeAd = [[MNGNativeAd alloc] init];
nativeAd.publisherId = @"YOUR_PUBLISHER_ID";
nativeAd.delegate = self;
    
```
##### Make a request 
To make a request you have to call loadAd 

```
[nativeAd loadAd];
```

##### Handle callBack from MNGNativeAdDelegate
```objc
-(void)nativeAdDidLoad:(MNGNativeAd *)nativeAd {
    NSLog(@"nativeAd did load");

    // You can now pull information from the nativeAd
    NSLog(@"app name: %@", [nativeAd title]);
    // etc


    // Once you create a view, "self.nativeView", to display your native ad, you can register it for impressions and click management
    [nativeAd registerViewForInteraction:self.nativeView withClickableView:self.nativeView];
}

-(void)nativeAd:(MNGNativeAd *)nativeAd didFailWithError:(NSError *)error {
    NSLog(@"nativeAd did fail with error : %@",error);    
}

-(void)nativeAdWasClicked:(MNGNativeAd *)nativeAd {
    // Called if you linked your view with registerViewForInteraction and the ad is clicked
    NSLog(@"nativeAd was clicked");
}

```

## Mopub

It is also possible to use the Mopub SDK and Mopub mediation to serve Appsfire ads using the mngads-server SDK.

Preliminary steps:

- Add the [MNGAds SDK for appsfire] to your Xcode project

- Add the [mngads-server Mopub adapter sources] (from the mopub-adapter folder) to your Xcode project 

- Create your app on the Mopub dashboard if that wasn't done already, and create inventory for fullscreen and native ads

- On your mopub dashboard, create a new order, set the type to network, and set the following class name   for interstitials:
MNGSushiInterstitialEvent

Pick your app and select interstitials

- On your mopub dashboard, create a new order, set the type to network, and set the following class name   

   for native ads:
   MNGNativeCustomEvent

   You do not need to set any other custom data on the dashboard.

- Initialize the publisher ID's for the MNG Appsfire placements

```objc
   #import "MNGNativeCustomEvent.h"
  #import "MNGSushiInterstitialEvent.h"
  ...

  // If you use interstitials
  [MNGSushiInterstitialEvent setPublisherID:@"MY_INTER_PUBLISHER_ID"];

  // If you use native ads
  [MNGNativeCustomEvent setPublisherID:@"MY_NATIVEAD_PUBLISHER_ID"];
```
- Use Mopub as usual

You may now use Mopub to show interstitials and native ads as usual. The adapter code and the setup you did on your Mopub dashboard will
allow MNG Appsfire ads to be mediated and served.


## Admob Mediation (certified)

You may also use the Admob SDK and [Admob mediation] to serve Appsfire ads using the mngads-server SDK.

Preliminary steps:


 - Add the [MNGAds SDK for appsfire] to your Xcode project
 - Add the mngads-server Admob adapter sources (from the admob-adapter folder) to your Xcode project. If not done yet, also add the GoogleMobileAds framework to serve Admob ads, and the Admob mediation support files that ship together with the GoogleMobileAds SDK: GADMAdNetworkAdapterProtocol.h, GADMAdNetworkConnectorProtocol.h and GADMEnums.h

 - Create your app in the Monetize tab of the Admob dashboard if that wasn't done already, and create an interstitial ad unit for your app.

 - On your Admob dashboard, for the interstitial ad unit, add a new ad source, select Appsfire from the list of networks. Enter 1 for the SDK token and again 1 for the secret key; they aren't used by MNGAds anymore but still need to be set to a value. 

 - Initialize the publisher ID's for the MNG Appsfire placements

```objc
#import "GADMAdapterAppsfire.h"

...

[GADMAdapterAppsfire setPublisherID:@"MY_MNG_PUBLISHER_ID"];

```

 - Use Admob as usual

You may now use Admob to show interstitials as usual. The adapter code and the setup you did on your Admob dashboard will allow MNG Appsfire ads to be mediated and served.

Interstitial example for Admob (not specific to MNG/Appsfire):

```objc
// Admob interstitial
GADInterstitial *interstitial;

...

// Load interstitial
// If the mediation is configured as such, this will load an MNG Appsfire ad

self.interstitial = [[GADInterstitial alloc] initWithAdUnitID:ADMOB_ADUNIT_ID];
self.interstitial.delegate = self;
[self.interstitial loadRequest:[GADRequest request]];

...
// Show interstitial

if ([self.interstitial isReady])
[self.interstitial presentFromRootViewController:self];
```



[Sushi]:http://docs.appsfire.com/sdk/ios/integration-reference/img/doc/sushi.mp4
[Sashimi]:http://docs.appsfire.com/sdk/ios/integration-reference/img/doc/sashimi-extended-light.jpg
[mngads-server Mopub adapter sources]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/mopub-adapter/?at=master
[MNGAds SDK for appsfire]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/MNGAds/MNGAds/?at=master
[Cocoapods]:http://cocoapods.org/
[Admob mediation]:https://developers.google.com/admob/android/mediation-networks#supported-ad-networks
