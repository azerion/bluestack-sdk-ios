![MNG-Ads-1.png](https://bitbucket.org/repo/aen579/images/3739691856-MNG-Ads-1.png) iOS for
![4193248577-af.png](https://bitbucket.org/repo/aen579/images/2031262448-4193248577-af.png) only


[TOC]

# Introduction

MNG Ads can be used for appsfire nativeAds only.

 - http://appsfire.com/

The Monetization features of Appsfire SDK allows you to display ads in your application:

 
 - Interstitial ads, A full-screen native ad unit for iPhone & iPad, we call it the [Sushi].
 - An in-stream native ad unit which allows you to deeply integrate our ads in your application's design, we call it [Sashimi]. 
## Start Integrating MNGAds Server

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
```
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
```
if (interNativeAd != nil) {
    interViewController = [interNativeAd getSushiViewController];
    interViewController.viewController = myViewController;  // Present from your view controller
    interViewController.delegate = self;
    [interViewController present];
}
```

##### Handle callBack from MNGSushiViewDelegate

-(void)interstitialDidAppear:(nonnull MNGSushiViewController *)sushiViewController {
    NSLog (@"interstitialDidAppear");
}

-(void)interstitialWasClicked:(nonnull MNGSushiViewController *)sushiViewController {
    NSLog (@"interstitialWasClicked");
}

-(void)interstitialWillDisappear:(nonnull MNGSushiViewController *)sushiViewController {
    NSLog (@"interstitialWillDisappear");
}

### Mopub

It is also possible to use the Mopub SDK and Mopub mediation to serve Appsfire ads using the mngads-server SDK.

Preliminary steps:

1. Add the mngads-server Mopub adapter sources (from the mopub-adapter folder) to your Xcode project 

2. Create your app on the Mopub dashboard if that wasn't done already, and create inventory for fullscreen and native ads

3. On your mopub dashboard, create a new order, set the type to network, and set the following class name for interstitials:
MNGSushiInterstitialEvent

Pick your app and select interstitials

4. On your mopub dashboard, create a new order, set the type to network, and set the following class name for native ads:
MNGNativeCustomEvent

You do not need to set any other custom data on the dashboard.

5. Initialize the publisher ID's for the MNG Appsfire placements

```objc
#import "MNGNativeCustomEvent.h"
#import "MNGSushiInterstitialEvent.h"
...

// If you use interstitials
[MNGSushiInterstitialEvent setPublisherID:@"MY_INTER_PUBLISHER_ID"];

// If you use native ads
[MNGNativeCustomEvent setPublisherID:@"MY_NATIVEAD_PUBLISHER_ID"];

7. Use Mopub as usual

You may now use Mopub to show interstitials and native ads as usual. The adapter code and the setup you did on your Mopub dashboard will
allow MNG Appsfire ads to be mediated and served.
```



[Sushi]:http://docs.appsfire.com/sdk/ios/integration-reference/img/doc/sushi.mp4
[Sashimi]:http://docs.appsfire.com/sdk/ios/integration-reference/img/doc/sashimi-extended-light.jpg