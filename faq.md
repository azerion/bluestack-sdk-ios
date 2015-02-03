# MngAds FAQ #

This document answers the following frequently asked questions:

[TOC]
# Implementation #
## What types of ad units are available? ##
There are three ad units available to use in your app:

 - Standard banner ads
 - Interstitial ads
 - Native ad API

## How many placement IDs should I create? ##
You need to create a different placement ID for any of the different ad formats (banner, interstitial and native) and each unique path that you implement within your app. 
If you use native ads in feed and plan to show several units as the user scrolls, then you should use the same placement ID for all the native ad units.
## What are "Native Ads ##
Native ads allow you to customize the look and feel of ads to match that of your app. Native ads work by receiving the metadata for ads through MngAds.

## How do I hide the status bar on Interstitials ? ##
Some Ads Network, provide an SDK where **ads are not presented modally by a view controller object**. Therefore, in order to prevent  this issue, you must used : 

```
#!objective-c

-(void)adsAdapterInterstitialDisappear:(MNGAdsAdapter *)adsAdapter
{
    NSLog(@"MngAds adsAdapterInterstitialDisappear");
    [[UIApplication sharedApplication] setStatusBarHidden:NO withAnimation:UIStatusBarAnimationSlide];
    UIViewController *vc = [[UIViewController alloc] init];
    [self.currentVC presentViewController:vc animated:NO completion:nil];
    [self.currentVC dismissViewControllerAnimated:NO completion:nil];
}
```
## How do I resize banners ? ##


```
#!objective-c

(void)adsAdapter:(MNGAdsAdapter )adsAdapter bannerDidLoad:(UIView )adView {
    NSLog(@"MngAds Banner: did load ad");
    UIView *bannerView;
    bannerView = adView;
    if ([bannerView isKindOfClass:[AFAdSDKSashimiView class]]) {
        CGRect frame = bannerView.frame;
        frame.size.height = 70;
        bannerView.frame = frame;
    }
    if (self.mngPerfBannerView.superview) {
        [self.mngPerfBannerView removeFromSuperview];
        self.mngPerfBannerView = nil;
    }
    [self.currentVC.view addSubview:bannerView];
}
```


# Publisher Application Process #
# Support #