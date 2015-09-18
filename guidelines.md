[TOC]
# Best practice Mngads : optimized use case for several ad formats on one page

mngAds| Description| 
------------- | ------------- |
![IMG_0363.PNG](https://bitbucket.org/repo/aen579/images/3282511754-IMG_0363.PNG) | When trying to display several ad formats on one page try to synchronize your requests instead of making multiple ones at the some time. By making the requests at the same time you are decreasing your chance of receving an Ad and you are making your app slow .You can check the number of MNGAdsFactory running a request by calling or use delegate like [FourInOneViewController.m](https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/FourInOneViewController.m?at=master) :

```objc
if([MNGAdsSDKFactory numberOfRunningFactory] <= MAX_ALLOWED_FACTORIES){
	//send your request
}
```

# Design Guidelines for MNG Ads

## Banner -  (50px or 90px)
Banner -  (50px or 90px) | Description| 
------------- | ------------- |
![IMG_0765-min.png](https://bitbucket.org/repo/aen579/images/4036275966-IMG_0765-min.png) | A banner is a small bar ad that appears at the bottom or top of your content. Usually sized 320 x 50. Only include one ad per page or show one ad at a time if scrolling. In all cases, **the banner width is flexible with a minimum of 320px.**. If you are building your app for iPad  consider using 90px and 50px for iphone.

## Square - Medium rectangle (300 x 250)

Square - Medium rectangle (300 x 250) | Description| 
------------- | ------------- |
![IMG_0764-min.PNG](https://bitbucket.org/repo/aen579/images/3928827332-IMG_0764-min.PNG) |Square banner also known as a *medium rectangle* (300 x 250). This format can increase earnings when both text and image ads are enabled. Performs well when embedded within text content or at the end of articles.

## Interstitial
Interstitial | Description| 
------------- | ------------- |
![IMG_0362.PNG](https://bitbucket.org/repo/aen579/images/1010762236-IMG_0362.PNG) | An interstitial is a full screen ad that appears at a natural transition point in your app.

## Native Ad

A native ad is a custom designed ad that fits seamlessly with your app. If done well, ads can blend in naturally with your interface.


Facebook  | Facebook  | Appsfire | carousel Ad
------------- | ------------- | -------------  | -------------
![nativeAd-FB.PNG](https://bitbucket.org/repo/aen579/images/742207682-nativeAd-FB.PNG) | ![IMG_0352.PNG](https://bitbucket.org/repo/aen579/images/3215310297-IMG_0352.PNG)| ![nativeAd-AF.PNG](https://bitbucket.org/repo/aen579/images/1328641730-nativeAd-AF.PNG)|![carousel.PNG](https://bitbucket.org/repo/aen579/images/2861407784-carousel.PNG)