# iOS DFP Adapter
[TOC]

This guide shows you how to integrate [MNGAds] mediation adapter of Google Mobile Ads SDK with your current iOS app and set up additional request parameters.

## Supported ad formats
- Banners
- Interstitials
- Native Ads

## Requirements
- Use Xcode 13 or higher
- Target iOS 12.2 or higher

## Google Ad Manager UI 

The custom event must be defined in the [Google Ad Manager UI].

### 1. Create a Yield groups

- Create an Ad Network
![screenshot-admanager.google.com-2019.10.02-22_36_16 (1).jpg](https://bitbucket.org/repo/GyRXRR/images/2101314984-screenshot-admanager.google.com-2019.10.02-22_36_16%20%281%29.jpg)

1. Create a Company with **Madvertise Ad-Network** name
2. Choose **Appsfire** network
3. Allow mediation

### 2. Add a Yield Group

![screenshot-admanager.google.com-2019.10.08-18_32_29.jpg](https://bitbucket.org/repo/aen579/images/3579724023-screenshot-admanager.google.com-2019.10.08-18_32_29.jpg)

1. Choose a name
2. Choose a format (You must create a Yield Group by format)
3. Choose at least one size according format
4. Target a specific placement

### 3. Add A Yield Partner and Define a custom event

On your Google Ad Manager UI, create a custom event 

![screenshot-admanager.google.com-2019.10.08-18_33_45.jpg](https://bitbucket.org/repo/aen579/images/837721569-screenshot-admanager.google.com-2019.10.08-18_33_45.jpg)

1. Select **Madvertise Ad-Network** created on [Step 1]
2. Choose **Custom Event** for Integration type
3. Choose your platform iOS or Android
4. Set the following **Label**, **class Name**  and **Parameter** according your format :

* Banner : Label= **GADBlueStackMediationAdapter**, class Name= **GADBlueStackMediationAdapter** and Parameter= /YOUR_APP_ID/PLACEMENT_ID_BANNER
* Interstitial : Label= **GADBlueStackMediationAdapter**, class Name= **GADBlueStackMediationAdapter** and Parameter= /YOUR_APP_ID/PLACEMENT_ID_INTER
* Native Ad : Label= **GADBlueStackMediationAdapter**, class Name= **GADBlueStackMediationAdapter** and Parameter= /YOUR_APP_ID/PLACEMENT_ID_NATIVEAD
* Square Ad : Label= **GADBlueStackMediationAdapter**, class Name= **GADBlueStackMediationAdapter** and Parameter= /YOUR_APP_ID/PLACEMENT_ID_SQUARE
* RewardVideo Ad : Label= **GADBlueStackMediationAdapter**, class Name= **GADBlueStackMediationAdapter** and Parameter= /YOUR_APP_ID/PLACEMENT_ID_REWARD_VIDEO

## Integrate Bluestack in your application project

### 1. Set Up

* check [Using CocoaPods] or [Manual Install] in order include Bluestack SDK on your application project.

* check [GoogleMobileAds-Adapter] and add manually on  your application project. 

* import Adapter files in your code :

```objc
#import "GADBlueStackMediationAdapter.h"
@import GoogleMobileAds;
 
```

### 2. Initialize your ads

You can check our [Madvertise Custom Events adapters Demo] page.

#### 2.1 Ads formats:

You may now use MNG DFP Adaptor to show Interstitial Ads and Banner Ads the same way it's described in the DFP Documentation.The adapter code and the setup you did on your Google Ad Manager UI will allow BlueStack Ads to deliver ads.

##### Since BlueStack V4.0.0 and Google-Mobile-Ads-SDK V9.0.0 :
  
   * Migrate With the DFP Documentation: [Prepare SDK v9 ]

 * **Banner/Sqaure:** GADBlueStackMediationAdapter :

    Before you can create custom events, you need to [integrate the banner ad format into your app].

   **PS: You must Passed the ViewController to the GADBannerView**:

     
```objc
  Objective-C : 

       GADBannerView *bannerView;
        ......................
       _bannerView.rootViewController = self;


  Swift :
      var bannerView: GAMBannerView!
      bannerView.rootViewController = self

``` 
 * **Interstitial:** GADBlueStackMediationAdapter :

    Before you can create custom events, you need to [integrate the Interstitial ad format into your app].

   **PS : In the Interstitial Ad inplementation you must Passed the ViewController to the Adapter**:**
  

```objc
  Objective-C : 

        [GADBlueStackMediationAdapter setViewController:self];


  Swift :
         GADBlueStackMediationAdapter.setViewController(self)

``` 


 * **Native Ads:** GADBlueStackMediationAdapter :

    Before you can create custom events, you need to [integrate the Native ad format into your app].

    **PS:  In the Native Ad inplementation you must Passed the ViewController to the GADBlueStackMediationAdapter**:** 

   ##### Init GADBlueStackMediationAdapter : 

```objc
  Objective-C : 

        [GADBlueStackMediationAdapter setViewController:self];


  Swift :
         GADBlueStackMediationAdapter.setViewController(self)

``` 
* **Rewarded video Ads:** GADBlueStackMediationAdapter :

    Before you can create custom events, you need to [integrate the Rewarded video ad format into your app].

    **PS:  In the Rewarded video inplementation you must Passed the ViewController to the GADBlueStackMediationAdapter**:** 

   ##### Init GADBlueStackMediationAdapter : 

```objc
  Objective-C : 

        [GADBlueStackMediationAdapter setViewController:self];


  Swift :
         GADBlueStackMediationAdapter.setViewController(self)

``` 


### 3. Custom targeting  / Keyword

   If you need to send Custom targetting /keywork
  import  BlueStackGADAdNetworkExtras class
```objc
 #import "BlueStackGADAdNetworkExtras.h"

```

  If you need to send your custom key-value pairs. You can specify key-value-targeting and keywords information in the ad request as follows,and you must send your custom key-value pairs also as follows,add the extras to the registerAdNetworkExtras method as follows:
  **Example:** 
```objc
    GAMRequest* request = [GAMRequest request];
    BlueStackGADAdNetworkExtras * extras = [[BlueStackGADAdNetworkExtras alloc] init];
    extras.keywords = @"target=mngadsdemo;version=4.1.0";
    extras.customTargetingBlueStack = @{@"age" :@"25"};
    [request registerAdNetworkExtras:extras];

```
[Using CocoaPods]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Home#markdown-header-using-cocoapods
[Manual Install]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Home#markdown-header-manual-install
[DFP Documentation]:https://developers.google.com/ad-manager/mobile-ads-sdk/ios/quick-start
[Google Ad Manager UI]:https://admanager.google.com/
[Step 1]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/dfp-adapter-ios#markdown-header-1-create-a-yield-groups
[Madvertise Custom Events adapters Demo]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/master/Demo/MNG-Ads-SDK/DFPDemoViewController.m
[Banner Ads]:https://developers.google.com/ad-manager/mobile-ads-sdk/ios/banner
[Interstitial Ads]:https://developers.google.com/ad-manager/mobile-ads-sdk/ios/interstitial
[Native Ads Documentation]:https://developers.google.com/ad-manager/mobile-ads-sdk/ios/native/advanced
[Demo]: https://bitbucket.org/mngcorp/mngads-demo-ios/src/master/Demo/MNG-Ads-SDK/GoogleMobileAds-Adapter_Demo/
[GoogleMobileAds-Adapter]: https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/GoogleMobileAds-Adapter-v4.1.0.zip
[Interstitial Ads]:https://developers.google.com/ad-manager/mobile-ads-sdk/ios/interstitial
[Banner Ads]:https://developers.google.com/ad-manager/mobile-ads-sdk/ios/banner
[Prepare SDK v9 ]:https://developers.google.com/ad-manager/mobile-ads-sdk/ios/migration?hl=en
[integrate the banner ad format into your app]:https://developers.google.com/ad-manager/mobile-ads-sdk/ios/banner?hl=en
[integrate the Interstitial ad format into your app]:https://developers.google.com/ad-manager/mobile-ads-sdk/ios/interstitial
[integrate the Native ad format into your app]:https://developers.google.com/ad-manager/mobile-ads-sdk/ios/native/start
[integrate the Rewarded video ad format into your app]:https://developers.google.com/ad-manager/mobile-ads-sdk/ios/rewarded