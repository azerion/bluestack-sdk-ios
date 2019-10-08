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
* Banner : Label= **MadvertiseCustomEventInterstitial**, class Name= **MadvertiseCustomEventInterstitial** and Parameter= /YOUR_APP_ID/PLACEMENT_ID_INTER
* Banner : Label= **MadvertiseCustomEventNativead**, class Name= **MadvertiseCustomEventNativead** and Parameter= /YOUR_APP_ID/PLACEMENT_ID_NATIVEAD


## Integrate MNGAds in your application project

### 1. Set Up

* check [Using CocoaPods] or [Manual Install] in order include MNGAds SDK on your application project.
* import [Madvertise Custom Events adapters] in your code :

```objc
 import "MadvertiseCustomEventInterstitial.h"
 import "MadvertiseCustomEventBanner.h"
 import "MadvertiseCustomEventNativead.h"
 
```
 



### 2. Initialize your ads

#### Init Preférence
we initialize the preferences to be used for the request for differents types of Ads.

```objc

-(DFPRequest*)prepareDFPRequest{
    MNGPreference *preferences = [Utils getTestPreferences];
       
       DFPRequest* request = [DFPRequest request];
       request.customTargeting = @{@"location" :preferences.location ,
                                   @"gender" : @(preferences.gender),
                                   @"keyWord" : preferences.keyWord
       };
    return request;
}


```

####  Banner


##### Init GADBannerView

To create a banner you have to init an object with type GADBannerView and set the GADBannerViewDelegate and the viewController.

```objc
   bannerAdView = [[GADBannerView alloc]
         initWithAdSize:kGADAdSizeBanner];
   bannerAdView.adUnitID = @"AdUnitId";
   bannerAdView.rootViewController = self;
   [MadvertiseCustomEventBanner setViewController:self];
    
    DFPRequest* request = [self prepareDFPRequest];
    
   [bannerAdView loadRequest:request];
```

##### Handle the Request from DFP

the DFP will call your CustomEventBanner Class and will enter to this method :

```objc
   - (void)requestBannerAd:(GADAdSize)adSize
              parameter:(NSString *)serverParameter
                  label:(NSString *)serverLabel
                request:(GADCustomEventRequest *)request {
     if (_viewController == nil) {
          return;
        }
   _bannerFactory = [[MNGAdsSDKFactory alloc]init];
        _bannerFactory.bannerDelegate = self;
        _bannerFactory.viewController = [self.delegate viewControllerForPresentingModalView];
        _bannerFactory.placementId = serverParameter;
        
        _bannerFactory.clickDelegate = self;
        
       MNGPreference *preferences = [Utils getTestPreferences];
       MNGAdSize size;
        if (GADAdSizeEqualToSize(adSize,kGADAdSizeLargeBanner)) { //SQUARE
            size = kMNGAdSizeLargeBanner;
        }else {
            if (GADAdSizeEqualToSize(adSize,kGADAdSizeMediumRectangle)) {
                 size = kMNGAdSizeMediumRectangle;
            } else {
                if (GADAdSizeEqualToSize(adSize,kGADAdSizeFullBanner)) {
                     size = kMNGAdSizeFullBanner;
                } else {
                      BOOL isIPAD = ([[UIDevice currentDevice] userInterfaceIdiom] == UIUserInterfaceIdiomPad);
                      size = (isIPAD)?kMNGAdSizeDynamicLeaderboard:kMNGAdSizeDynamicBanner;
                }
            }
        }
    
        [_bannerFactory loadBannerInFrame:size withPreferences:preferences];
                
}
   
```

##### Handle callBack from GADBannerViewDelegate
adViewDidReceiveAd: will be called by the SDK when your bannerView is ready. now you can add your adView to th ViewHierarchy.

```objc
/// Tells the delegate an ad request loaded an ad.
-(void)adsAdapter:(MNGAdsAdapter *)adsAdapter bannerDidLoad:(UIView *)adView preferredHeight:(CGFloat)preferredHeight {

   int width = _viewController.view.frame.size.width;
    adView.frame = CGRectMake( 0, [[UIScreen mainScreen] bounds].size.height - preferredHeight, width, preferredHeight);
    adView.autoresizingMask = UIViewAutoresizingFlexibleHeight | UIViewAutoresizingFlexibleWidth;
    DFPDemoViewController* dfpDemoVC  = (DFPDemoViewController*)_viewController ;
    if (dfpDemoVC.bannerFromMNGView) {
        [dfpDemoVC.bannerFromMNGView removeFromSuperview];
    }
    dfpDemoVC.bannerFromMNGView = adView;
    dispatch_async(dispatch_get_main_queue(), ^{
        [_viewController.view addSubview:adView];
    });
    
   }

```

adView: didFailToReceiveAdWithError: will be called when ad  request fail. it will return the error of last called ad request.

```objc
/// Tells the delegate an ad request failed.
-(void)adsAdapter:(MNGAdsAdapter *)adsAdapter bannerDidFailWithError:(NSError *)error{
    if ([self.delegate respondsToSelector:@selector(customEventBanner:didFailAd:)]) {
        [self.delegate customEventBanner:self didFailAd:error];
    }
    
}

```
#### Interstitial

##### Init GADInterstitial

To create an interstitial you must init an object with type GADInterstitial and set the GADInterstitialDelegate and the viewController.

```objc
    interstitial = [[GADInterstitial alloc] initWithAdUnitID:@"AdUnitId"];
    interstitial.delegate = self;
    DFPRequest* request = [self prepareDFPRequest];
    [interstitial loadRequest:request];
```
##### Handle the Request from DFP

the DFP will call your CustomEventInterstitial  Class and will enter to this method :

```objc
 - (void)requestInterstitialAdWithParameter:(NSString *)serverParameter
                                     label:(NSString *)serverLabel
                                   request:(GADCustomEventRequest *)request {
      if (_interFactory.isBusy) {
          NSLog(@"Ads Factory is busy");
          return;
      }
      
      _interFactory = [[MNGAdsSDKFactory alloc]init];
      _interFactory.interstitialDelegate = self;
      _interFactory.placementId =  serverParameter ; 
      _interFactory.viewController = [[[[UIApplication sharedApplication]delegate] window]rootViewController];
      _interFactory.clickDelegate = self;
      
      [_interFactory loadInterstitialAutoDisplayed:YES];
    
    
}
```

##### Handle callBack from GADInterstitialDelegate
interstitialDidReceiveAd: will be called by the SDK when your Interstitial is ready. Interstitial will be showen.

```objc
-(void)adsAdapterInterstitialDidLoad:(MNGAdsAdapter *)adsAdapter {
    if ([self.delegate respondsToSelector:@selector(customEventInterstitialDidReceiveAd:)]) {
        [self.delegate customEventInterstitialDidReceiveAd:self];
    }
}

```

adsAdapter: didFailToReceiveAdWithError: will be called when  ad request fail. it will return the error of last called ad request.


```objc
-(void)adsAdapter:(MNGAdsAdapter *)adsAdapter interstitialDidFailWithError:(NSError *)error {
    if ([self.delegate
         respondsToSelector:@selector(customEventInterstitial:didFailAd:)]) {
        [self.delegate customEventInterstitial:self didFailAd:error];
    }
}
```

 Tells the delegate that an interstitial will be presented.

```objc
- (void)interstitialWillPresentScreen:(DFPInterstitial *)ad {
  NSLog(@"interstitialWillPresentScreen");
  }

```


#### Native Ads 

##### Init MadvertiseCustomEventNativead

To create a nativeAd  you have to init an object with type MadvertiseCustomEventNativead and set the GADNativeCustomTemplateAdLoaderDelegate.

```objc
     [MadvertiseCustomEventNativead setMainImage:_mainImageView andIconeImage:_iconImageView andNativeView:_nativeView andButton:_callToActionLabel andWithViewController:self andTitleLabel:_titleLabel andMainLabel:_mainTextLabel];
     GADNativeAdViewAdOptions *adViewOptions = [[GADNativeAdViewAdOptions alloc] init];
     adLoader = [[GADAdLoader alloc] initWithAdUnitID:@"AdUnit" rootViewController:self adTypes:@[kGADAdLoaderAdTypeUnifiedNative] options:@[adViewOptions]];
     adLoader.delegate = self;
     DFPRequest* request = [self prepareDFPRequest];
     [adLoader loadRequest:request];
```

##### handle the request from DFP
the DFP will call your CustomEventNativeAd  Class and will enter to this method :

```objc
    - (void)requestNativeAdWithParameter:(NSString *)serverParameter
                             request:(GADCustomEventRequest *)request
                             adTypes:(NSArray *)adTypes
                             options:(NSArray *)options
                  rootViewController:(UIViewController *)rootViewController {
  BOOL requestedUnified = [adTypes containsObject:kGADAdLoaderAdTypeUnifiedNative];

  // This custom event assumes you have implemented unified native advanced in your app as is done
  // in this sample.

  if (!requestedUnified) {
    NSString *description = @"You must request the unified native ad format.";
    NSDictionary *userInfo =
        @{NSLocalizedDescriptionKey : description, NSLocalizedFailureReasonErrorKey : description};
    NSError *error =
        [NSError errorWithDomain:@"com.google.mediation.sample" code:0 userInfo:userInfo];
    [self.delegate customEventNativeAd:self didFailToLoadWithError:error];
    return;
  }

  // This custom event uses the server parameter to carry an ad unit ID, which is the most common
  // use case.
    if (_nativeFactory != nil) {
        [_nativeFactory releaseMemory];
        _nativeFactory = nil;
    }
    
    _nativeFactory = [[MNGAdsSDKFactory alloc]init];
    _nativeFactory.nativeDelegate = self;
    _nativeFactory.viewController = _viewController;
    _nativeFactory.placementId =  serverParameter ; //_nativePlacement;
    _nativeFactory.clickDelegate = self;
    
    [_nativeFactory loadNative];
}
```

##### Handle callBack from NativeDelegate
adLoaderDidFinishLoading: will be called by the SDK when your nativeObject is ready. now you can create your own view.

```objc
- (BOOL)handlesUserClicks {
    return NO;
}


- (BOOL)handlesUserImpressions {
    return NO;
}


-(void)adsAdapter:(MNGAdsAdapter *)adsAdapter nativeObjectDidLoad:(MNGNAtiveObject *)adView{
    SampleMediatedNativeAd *mediatedAd =
    [[SampleMediatedNativeAd alloc] initWithSampleNativeAd:adView
                                     nativeAdViewAdOptions:_nativeAdViewAdOptions];
    [self.delegate customEventNativeAd:self didReceiveMediatedUnifiedNativeAd:mediatedAd];
    
    //set the graphics
    dispatch_async(dispatch_get_main_queue(), ^{
        _nativeView.hidden = NO;
        [_callToActionLabel setTitle:adView.callToAction forState:UIControlStateNormal];
        _titleLabel.text = adView.title;
        _mainTextLabel.text = adView.body;
         [adView registerViewForInteraction:_nativeView withMediaView:_mainImageView withIconImageView:_iconImageView withViewController:_viewController withClickableView:_callToActionLabel];
    });

}

```
adLoader:didFailToReceiveAdWithError: will be called when all ad request fail. it will return the error of last called ad request.

```objc

- (void)adsAdapter:(MNGAdsAdapter *)adsAdapter nativeObjectDidFailWithError:(NSError *)error{
    [self.delegate customEventNativeAd:self didFailToLoadWithError:error];
}

```

[Using CocoaPods]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Home#markdown-header-using-cocoapods
[Manual Install]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Home#markdown-header-manual-install
[mngads-dfp-adapter-1.0.0.aar]:https://bitbucket.org/mngcorp/mngads-demo-android/src/HEAD/MopubDemo/app/libs/mngads-mopub-adapter.aar?at=master&fileviewer=file-view-default
[mngads-sdk-x.aar Android SDK]:https://bitbucket.org/mngcorp/mngads-demo-android/src/HEAD/MngAdsDemo/app/libs/mngads-sdk-2.7.aar?at=master
[DFP Documentation]:https://developers.google.com/ad-manager/mobile-ads-sdk/ios/quick-start
[Google Ad Manager UI]:https://admanager.google.com/
[Step 1]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/dfp-adapter-ios#markdown-header-1-create-a-yield-groups
[Madvertise Custom Events adapters] :https://bitbucket.org/mngcorp/mngads-demo-ios/src/master/Demo/MNG-Ads-SDK/GoogleMobileAds-Adapter/