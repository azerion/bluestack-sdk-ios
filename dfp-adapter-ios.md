# iOS DFP Adapter
[TOC]

This guide shows you how to integrate [MNGAds] mediation adapter of Google Mobile Ads SDK with your current iOS app and set up additional request parameters.

## Supported ad formats
- Banners
- Interstitials
- Native Ads

## Requirements
- Use Xcode 11 or higher
- Target iOS 10.0 or higher

## Google Ad Manager UI 

The custom event must be defined in the [Google Ad Manager UI].

### 1. Create a Yield groups

- Create an Ad Network
![screenshot-admanager.google.com-2019.10.02-22_36_16 (1).jpg](https://bitbucket.org/repo/GyRXRR/images/2101314984-screenshot-admanager.google.com-2019.10.02-22_36_16%20%281%29.jpg)

1. Create a Company with **Madvertise Ad-Network** name
2. Choose **Appsfire** network
3. Allow mediation


![screenshot-admanager.google.com-2019.10.02-22_32_42.jpg](https://bitbucket.org/repo/GyRXRR/images/3231118223-screenshot-admanager.google.com-2019.10.02-22_32_42.jpg)

### 2. Define a custom event

On your Google Ad Manager UI, create a custom event 

![screenshot-admanager.google.com-2019.10.02-22_33_13.jpg](https://bitbucket.org/repo/GyRXRR/images/1642703664-screenshot-admanager.google.com-2019.10.02-22_33_13.jpg)

![screenshot-admanager.google.com-2019.10.02-22_36_16.jpg](https://bitbucket.org/repo/GyRXRR/images/4019010383-screenshot-admanager.google.com-2019.10.02-22_36_16.jpg)

![l.png](https://bitbucket.org/repo/GyRXRR/images/3601965291-l.png)

## Integrate MNGAds in your application project

### 1. Set Up

* Add our adapter [mngads-dfp-adapter-1.0.0.aar]
* check [Using CocoaPods] or [Manual Install] in order include MNGAds SDK on your application project.



### 2. Initialize your ads

#### Interstitials and Banners
// TBD


#### Native Ads 
// TBD


[Using CocoaPods]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Home#markdown-header-using-cocoapods
[Manual Install]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Home#markdown-header-manual-install
[mngads-dfp-adapter-1.0.0.aar]:https://bitbucket.org/mngcorp/mngads-demo-android/src/HEAD/MopubDemo/app/libs/mngads-mopub-adapter.aar?at=master&fileviewer=file-view-default
[mngads-sdk-x.aar Android SDK]:https://bitbucket.org/mngcorp/mngads-demo-android/src/HEAD/MngAdsDemo/app/libs/mngads-sdk-2.7.aar?at=master
[DFP Documentation]:https://developers.google.com/ad-manager/mobile-ads-sdk/ios/quick-start
[Google Ad Manager UI]:https://admanager.google.com/