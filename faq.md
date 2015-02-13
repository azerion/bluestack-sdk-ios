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

(void)adsAdapter:(MNGAdsAdapter *)adsAdapter bannerDidLoad:(UIView *)adView {
    NSLog(@"MngAds Banner: did load ad");
    UIView *bannerView;
    bannerView = adView;
    if ([bannerView isKindOfClass:[AFAdSDKSashimiView class]]) {
        CGRect frame = bannerView.frame;
        frame.size.height = 70;
        bannerView.frame = frame;
    }
//.
//.
//.
    [self.currentVC.view addSubview:bannerView];
}
```

## What IDFA related options do I need to choose when submitting my iOS app to Apple for review?

When you submit an iOS application on iTunes Connect, the service mobile developers use to distribute and update their applications on the iTunes App Store, Apple now explains how the Advertising Identifier (IDFA) can and cannot be used, and asks for developers’ compliance with these rules by checking a box.

If you do not want your application to be rejected by Apple, here are simple steps and precautions to take when you use the MngAds, Facebook, Google, Appsfire and MngPerf iOS SDKs.


 You must select the following options :

 - Serve advertisements within the app
 - Attribute this app installation to a previously served advertisement

>We advise you to explicitly tell Apple you are using MngAds iOS SDK in your application, and to provide the link to this documentation page.


MngAds uses following third party SDKs :

 - http://help.smartadserver.com/iOS/V5.0/#IntegrationGuides/Checklist.htm?Highlight=idfa
 - https://developers.facebook.com/docs/audience-network/faq?locale=fr_FR#a17
 - http://docs.appsfire.com/sdk/ios/integration-reference/Requirements/Submit_An_App_With_Appsfire_iOS_SDK
 - https://developers.google.com/mobile-ads-sdk/download#downloadios

# Publisher Application Process #
# Support #