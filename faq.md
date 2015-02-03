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

## How I hide the status bar on Interstitials ? ##
Some adNetwork do not provide a *Interestitial view controller (presented modally)*. Therefore, in order to prevent  this issue, you must used : 



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

# Publisher Application Process #
# Support #