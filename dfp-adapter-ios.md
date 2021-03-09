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

* Banner : Label= **MadvertiseCustomEventBanner**, class Name= **MadvertiseCustomEventBanner** and Parameter= /YOUR_APP_ID/PLACEMENT_ID_BANNER
* Interstitial : Label= **MadvertiseCustomEventInterstitial**, class Name= **MadvertiseCustomEventInterstitial** and Parameter= /YOUR_APP_ID/PLACEMENT_ID_INTER
* Native Ad : Label= **MadvertiseCustomEventNativead**, class Name= **MadvertiseCustomEventNativead** and Parameter= /YOUR_APP_ID/PLACEMENT_ID_NATIVEAD


## Integrate MNGAds in your application project

### 1. Set Up

* check [Using CocoaPods] or [Manual Install] in order include MNGAds SDK on your application project.

* check [GoogleMobileAds-Adapter] and add manually on  your application project. 

* since 
* import Adapter files in your code :

```objc

#import "MadvertiseCustomEventInterstitial.h"
#import "MadvertiseCustomEventBanner.h"
#import "MadvertiseCustomEventNativead.h"
@import GoogleMobileAds;
 
```

### 2. Initialize your ads

You can check our [Demo] page.

#### 2.1 Banner and Interstitial:

You may now use MNG DFP Adaptor to show Interstitial Ads and Banner Ads the same way it's described in the DFP Documentation.The adapter code and the setup you did on your Google Ad Manager UI will allow MNG Ads to deliver ads.

##### Since BlueStack V3.2.0 and Google-Mobile-Ads-SDK V8.0.0 

  * GADInterstitialDelegate is deprecated : use GADFullScreenContentDelegate 
  * DFPRequest is renamed to GAMRequest
  

 Migrate With the DFP Documentation: [Prepare SDK v8 ]

You must pass CUSTOMLABELADAPTER  with custom event adapter class name for  and Passed the ViewController to the Adapter:

 * **Banner :** MadvertiseCustomEventBanner :
 
```objc
    MadvertiseCustomEventBanner * customEventBanner = [[MadvertiseCustomEventBanner alloc] init];
    [customEventBanner setViewController:self];    
 
``` 
##### Handle callBack from GADBannerViewDelegate
  Through the use of GADBannerViewDelegate, you can listen for lifecycle events, such as when an ad is closed or the user leaves the app.
     
  * Registering for banner events :

```objc
    _bannerView.delegate = self;

``` 

 *  Tells the delegate an ad request loaded an ad:

```objc
- (void)adViewDidReceiveAd:(nonnull GADBannerView *)bannerView{

}

``` 

 *   Tells the delegate an ad request failed..

```objc
- (void)adView:(nonnull GADBannerView *)bannerView
didFailToReceiveAdWithError:(nonnull GADRequestError *)error{
    
}
``` 
#### Interstitial

 * **Interstitial :** MadvertiseCustomEventInterstitial :

 
```objc
 MadvertiseCustomEventInterstitial * customEventInterstitial = [[MadvertiseCustomEventInterstitial alloc]init];
    [customEventInterstitial setViewController: YourViewController];
    

``` 
##### Handle callBack from GADInterstitialDelegate

  *  set the GADInterstitialDelegate and the viewController and add "GADInterstitialDelegate" in the interface viewController :

```objc
_interstitial.delegate = self;

``` 

 *   will be called by the SDK when your Interstitial is ready. Interstitial will be showen:

```objc

- (void)interstitialWillPresentScreen:(GADInterstitial *)interstitial {
    
}
``` 

 *   interstitialWillDismissScreen: Called before the interstitial is to be animated off the screen.

```objc

-(void)interstitialWillDismissScreen:(GADInterstitial *)ad{
    
}
``` 

#### Native Ads 

##### Init MadvertiseCustomEventNativead

To create a nativeAd  you have to init an object with type MadvertiseCustomEventNativead and set the DFPNativeAdLoadedDelegate to the self view controller.

```objc
   [MadvertiseCustomEventNativead setMainImage:_mainImageView andIconeImage:_iconImageView andNativeView:_nativeView andButton:_callToActionLabel andWithViewController:self andTitleLabel:_titleLabel andMainLabel:_mainTextLabel];
    
    [MadvertiseCustomEventNativead setNativeAdMadvertiseDFPDelegate:self];
    
    GADNativeAdViewAdOptions *adViewOptions = [[GADNativeAdViewAdOptions alloc] init];
    adLoader = [[GADAdLoader alloc] initWithAdUnitID: NATIVE_AD_ADUNIT rootViewController:self adTypes:@[kGADAdLoaderAdTypeUnifiedNative] options:@[adViewOptions]];
   [MadvertiseCustomEventNativead setNativeAdMadvertiseDFPDelegate:self];

    DFPRequest* request = [DFPRequest request];
    CLLocation *currentLocation = _locationManager.location;
    if (currentLocation) {
        [request setLocationWithLatitude:currentLocation.coordinate.latitude
                               longitude:currentLocation.coordinate.longitude
                                accuracy:currentLocation.horizontalAccuracy];
    }
        request.keywords = [self setRequestKeyword:@"target=mngadsdemo;version=2.15.1"];

 request.customTargeting = @{@"key1" : @"key1vaule", @"key2" :@"key2vaule"};
    GADCustomEventExtras *extras = [[GADCustomEventExtras alloc] init];
    [extras setExtras:request.customTargeting forLabel:@"MadvertiseCustomEventNativead"];
    [request registerAdNetworkExtras:extras];
    [adLoader loadRequest:request];
```

##### Handle callBack from NativeAdMadvertiseDFPDelegate
madvertiseCustomEventNativeAdidReceiveAd: will be called when the nativeObject is ready. now you can create your own view.

```objc

-(void)madvertiseCustomEventNativeAdidReceiveAd:(MNGNAtiveObject *)nativeDFPObject{
    _nativeView.hidden = NO;
    [self.view bringSubviewToFront:_nativeView];
    [_callToActionLabel setTitle:nativeDFPObject.callToAction forState:UIControlStateNormal];
    _titleLabel.text = nativeDFPObject.title;
    _mainTextLabel.text = nativeDFPObject.body;
    [nativeDFPObject registerViewForInteraction:_nativeView withMediaView:_mainImageView withIconImageView:_iconImageView withViewController:self withClickableView:_callToActionLabel];
}
}

```
adLoader:didFailToReceiveAdWithError: will be called when all ad request fail. it will return the error of last called ad request.

```objc
-(void)madvertiseCustomEventNativeAd:(NSObject *)adapter didFailToLoadWithError:(NSError *)error{
    NSLog(@"native dfp Object did fail");
}

```

### 3. Location

- If a user has granted your app location permissions, Ad Manager automatically passes this location data to the SDK. The SDK uses this data to improve ad targeting without requiring any code changes in your app. 
- You can specify location-targeting information in the ad request as follows:

```objc
 DFPRequest* request = [DFPRequest request];
    CLLocation *currentLocation = _locationManager.location;
    if (currentLocation) {
        [request setLocationWithLatitude:currentLocation.coordinate.latitude
                               longitude:currentLocation.coordinate.longitude
                                accuracy:currentLocation.horizontalAccuracy];
    }
```

### 4. Custom targeting 

If you need to send your preferences (Age, Keyword, Content URL) use the GADCustomEventExtras  setExtras  method.
 
```objc
    DFPRequest* request = [DFPRequest request];
    request.customTargeting = @{@"key1" : @"key1vaule", @"key2" :@"key2vaule"};
    GADCustomEventExtras *extras = [[GADCustomEventExtras alloc] init];
    [extras setExtras:request.customTargeting forLabel:@"MadvertiseCustomEventBanner"];
    [request registerAdNetworkExtras:extras];
```





 
[Using CocoaPods]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Home#markdown-header-using-cocoapods
[Manual Install]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Home#markdown-header-manual-install
[mngads-dfp-adapter-1.0.0.aar]:https://bitbucket.org/mngcorp/mngads-demo-android/src/HEAD/MopubDemo/app/libs/mngads-mopub-adapter.aar?at=master&fileviewer=file-view-default
[mngads-sdk-x.aar Android SDK]:https://bitbucket.org/mngcorp/mngads-demo-android/src/HEAD/MngAdsDemo/app/libs/mngads-sdk-2.7.aar?at=master
[DFP Documentation]:https://developers.google.com/ad-manager/mobile-ads-sdk/ios/quick-start
[Google Ad Manager UI]:https://admanager.google.com/
[Step 1]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/dfp-adapter-ios#markdown-header-1-create-a-yield-groups
[Madvertise Custom Events adapters]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/master/Demo/MNG-Ads-SDK/GoogleMobileAds-Adapter/
[Banner Ads]:https://developers.google.com/ad-manager/mobile-ads-sdk/ios/banner
[Interstitial Ads]:https://developers.google.com/ad-manager/mobile-ads-sdk/ios/interstitial
[Native Ads Documentation]:https://developers.google.com/ad-manager/mobile-ads-sdk/ios/native/advanced
[Demo]: https://bitbucket.org/mngcorp/mngads-demo-ios/src/master/Demo/MNG-Ads-SDK/GoogleMobileAds-Adapter_Demo/
[GoogleMobileAds-Adapter]: https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/GoogleMobileAds-Adapter-v1.4.3.zip
[Interstitial Ads]:https://developers.google.com/ad-manager/mobile-ads-sdk/ios/interstitial
[Banner Ads]:https://developers.google.com/ad-manager/mobile-ads-sdk/ios/banner
[Prepare SDK v8 ]:https://developers.google.com/ad-manager/mobile-ads-sdk/ios/migration
