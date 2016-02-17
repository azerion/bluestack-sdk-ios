# MngAds FAQ #

This document answers the following frequently asked questions:

[TOC]
# IOS9

## Is bitcode supported?

v1.4.1 of the SDK supports bitcode. If you are using earlier versions, you must disable bitcode.

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

## How do I hide the status bar on Interstitials ? (for sdk version < 2.0.3) ##

**Only if you are using mngads < 2.0.3**

Since iOS8 you can manage the status bar appeareance on per screen basis.To change the status bar status you should change the property only on the screen that is taking the whole window.

If you are using a navigation controller this is on the navigation controller that it should be done. You'll need to subclass you navigation controller and override the prefersStatusBarHidden so that it return the top view controller prefersStatusBarHidden value.

```
#!objective-c
@interface MyNavigationController : UINavigationController

@end

@implementation MyNavigationController

-(BOOL)prefersStatusBarHidden{
    return self.topViewController.prefersStatusBarHidden;
}

@end
```

On your view controller using the callbacks you can determine the style and appearance of the status bar and then call the setNeedsStatusBarAppearanceUpdate on your navigation controller

```
#!objective-c
-(void)adsAdapterInterstitialDidLoad:(MNGAdsAdapter *)adsAdapter{
    ...
    [self setStatusBarHidden:YES];
}

-(void)adsAdapterInterstitialDisappear:(MNGAdsAdapter *)adsAdapter{
    ...
    [self setStatusBarHidden:NO];
    
}

- (void)setStatusBarHidden:(BOOL)hidden {
    self.statusBarHidden = hidden;
    
    [[UIApplication sharedApplication]setStatusBarHidden:hidden];
    if ([self.navigationController respondsToSelector:@selector(setNeedsStatusBarAppearanceUpdate)]) {
        [self.navigationController setNeedsStatusBarAppearanceUpdate];
    }
}

-(BOOL)prefersStatusBarHidden{
    return self.statusBarHidden;
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

## CocoaPods Troubleshooting

If you have those build errors: 
```
Library not found for -lMNGAds or -lAppNexusSDK
Header not found for ...
```

You have to check if:
- Header search paths
- Framework search paths
- Library search paths
- Other linker Flags

see http://guides.cocoapods.org/using/troubleshooting.html on .4

or use `ONLY_ACTIVE_ARCH = NO;` 

## duplicate symbol issue on Xcode 6.4

**FBAudienceNetwork.framework** and **libSmartAdServer.a** do not work with **Xcode 6.4**. Therefore, MngAds needs **Xcode 7**.

 - https://developers.facebook.com/bugs/752177668227984/

## Missing close button on interstitials ?

Do not avoid to add bundle of smart ( https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/sdk/sas.bundle/?at=master ).

## Undifined symbol with pod

SmartAdserver do not provide a pod, therefore you must add [libSmartAdServer.a] manually to your project 
 - https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Using%20CocoaPods


[libSmartAdServer.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/SASsdk/?at=master

## -Objc linker flag required:
For manual installation without pod, do not forget to include the "-ObjC" linker flag in "Other Linker Flags" under "Build Settings" in the project file." in order to avoid some crashes.

![flag-xcode.png](https://bitbucket.org/repo/aen579/images/658800622-flag-xcode.png)

## `MNGAds/MNGAdsFull` required by `Podfile`

if on pod install there is following error


```
#!ruby

`MNGAds/MNGAdsFull` required by `Podfile`
```

try 


```
#!ruby

sudo rm -fr ~/Library/Caches/CocoaPods/
sudo rm -fr ~/.cocoapods/repos/master/
```