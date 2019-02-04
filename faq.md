# MngAds FAQ #

This document answers the following frequently asked questions:

[TOC]

# IOS11

## iphone x and safe area

```
#!objective-c

adView.frame = CGRectMake(0, 0, width, preferredHeight); //O by default
if (@available(iOS 11.0, *)) {
if ([UIApplication sharedApplication].keyWindow.safeAreaInsets.top > 0.0) {
// iphone X and safe area
CGFloat safeAreaTopInset =[UIApplication sharedApplication].keyWindow.safeAreaInsets.top;
adView.frame = CGRectMake(0, safeAreaTopInset, width, preferredHeight);
}
}
```


# ATS

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
# IOS10

## NSCalendarsUsageDescription

On iOS 10+, the App Store’s [privacy policy] requires apps to provide a usage description when attempting to access privacy-sensitive data,sush as a user’s calendar. Info.plist must contain an NSCalendarsUsageDescription key with a string value explaining to the user how the app uses this data according to [Apple's guideline].

```
#!objective-c
<key>NSCalendarsUsageDescription</key>
<string>Some ad content may access calendar</string>
```

Other privacy-sensitive data are NSBluetoothPeripheralUsageDescription, NSCameraUsageDescription, NSContactsUsageDescription, NSHealthShareUsageDescription, see [Apple's guideline]

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

## Memory managment
When you have finished your ads plant you must free the memory.

When using [ARC] it will be done automatically. Otherwise you have to call "releaseMemory".
 - ARC
```objc
[adsFactory releaseMemory];//optional
adsFactory = nil;
```

 - Avoid crashes

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

## Delegate not called


**Don't use factory as local variable.**

```objc
-(BOOL)showInterstitial
{
    MNGAdsSDKFactory *interstitialAdsFactory = [[MNGAdsSDKFactory alloc]init];
    interstitialAdsFactory.interstitialDelegate = self;
    ...
    //at the end of this methode interstitialAdsFactory will be deallocated
}
```

If you do it, the factory will be deallocated in no time (so the request will be stopped). So you have to use property or global variable.

```objc
@implementation YOUR_CLASS{
    MNGAdsSDKFactory *_interstitialAdsFactory;
}

-(BOOL)showInterstitial
{
    _interstitialAdsFactory = [[MNGAdsSDKFactory alloc]init];
    _interstitialAdsFactory.interstitialDelegate = self;
    ...
}
```

## May slow down your iPhone popup

If you have a popup "May slow down your iPhone" that mean that your app did not support arch 64bit, so you have to add arm64 to Build settings -> valid architectures even if you put Build Valid Architecture Only NO.

![slow.png](https://bitbucket.org/repo/aen579/images/3334494345-slow.png)


## cocoapod ld: library not found for 

In this case, can you please check : 

 - http://guides.cocoapods.org/using/troubleshooting.html

If Xcode complains when linking, e.g. Library not found for -lPods, it doesn't detect the implicit dependencies:

Go to Product > Edit Scheme
Click on Build
Add the Pods static library, and make sure it's at the top of the list
Clean and build again

## Adapter not found after pod install

```
#!objective-c


sudo rm -rf "${HOME}/Library/Caches/CocoaPods" //clean cache
gem uninstall cocoapods 
gem install cocoapods
rm -rf ~/Library/Developer/Xcode/DerivedData
```


then
 

```
#!objective-c

use_frameworks!
pod "MNGAds" 
pod install
```
## Missing Architectures after pod update/install

- First make sure you have [git LFS](https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Home#markdown-header-requirements) installed on your machine
- you need to clear cocoapods's cache with this command :


```
#!objective-c
sudo rm -rf "${HOME}/Library/Caches/CocoaPods" 
```
afterwards remove MNGAds from your pod file , do a pod install so it deletes your current version of MNGAds , finally go back to the pod file and add MNGAds again and do a new pod install so it brings you a new version of MNGAds with the git lfs files.(this needs to be done just once)






## Muted sound

Recently some ads have caused some audio issues: where after the ad is dismissed the entire app becomes muted, and after a thourough investigation we discovered that the issue comes from an adnetwork we currently use and until they fix the issue on their end here s a workaround : what causes the issue is that when a video in an ad loads is changes the category of AVAudioSession's shared instance, so to avoid it you only need to revert (after the ad is dismissed) to the category you initially set, for example :


```
#!objective-c
-(void)adsAdapterInterstitialDisappear:(MNGAdsAdapter *)adsAdapter{

  [[AVAudioSession sharedInstance] setCategory:AVAudioSessionCategoryPlayback error:nil];
  [[AVAudioSession sharedInstance] setActive: YES error: nil];

}
```

## Interstial status bar with v2.10

"On info.plist if you are using "View controller-based status bar appearance" (UIViewControllerBasedStatusBarAppearance), it must be setted to No"

Or in case you don't want to change the value of UIViewControllerBasedStatusBarAppearance, then you can manually hide the status bar yourself since in some cases the interstitial will be shown using addSubview in the view of the viewController you passed to the factory.



[privacy policy]:https://developer.apple.com/app-store/review/guidelines/#privacy
[Apple's guideline]:https://developer.apple.com/library/prerelease/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW15
[App Transport Security]:https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW60
[extended the ATS deadline]:https://developer.apple.com/news/?id=12212016b&1482372961