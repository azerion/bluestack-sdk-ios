![mad_AdNetworkMediation_rgb_small.png](https://bitbucket.org/repo/GyRXRR/images/3981639300-mad_AdNetworkMediation_rgb_small.png) for IOS


# Banner Integration for IOS

[TOC]

## Overview
Before You Start. Make sure that you have correctly integrated the MNG SDK into your application. Integration is outlined [here](https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/setup).

## Step 1. Init Banner factory

To create a banner you have to init an object with type MNGAdsSDKFactory and set the bannerDelegate and the viewController.

**Objective-C**

```objc
bannerAdsFactory = [[MNGAdsSDKFactory alloc]init];
bannerAdsFactory.bannerDelegate = self;
bannerAdsFactory.viewController = self;
```
**Swift**

```Swift
bannerAdsFactory = MNGAdsSDKFactory()
bannerAdsFactory.viewController = self
bannerAdsFactory.bannerDelegate = self
```
You have also to set placementId (minimum one time)
**Objective-C**

```objc
bannerAdsFactory.placementId = @"/YOUR_APP_ID/PLACEMENT_ID";
```
**Swift**

```Swift
 bannerAdsFactory.placementId = "/YOUR_APP_ID/PLACEMENT_ID"
```

## Step 2. Make a request
To make a request you have to call 'loadBannerInFrame'.

**Objective-C**

```objc
[bannerAdsFactory loadBannerInFrame:kMNGAdSizeDynamicBanner]

```

**Swift**

```Swift

 bannerFactory.loadBanner(inFrame: CGRect(x:0, y:60,width:self.view.frame.size.width,height: 50), withPreferences: preference)
 
```



## Step 3. Handle callBack from BannerDelegate
adsAdapter:bannerDidLoad: will be called by the SDK when your bannerView is ready. now you can add your bannerView to th ViewHierarchy.

**Objective-C**

```objc
-(void)adsAdapter:(MNGAdsAdapter  *)adsAdapter bannerDidLoad:(UIView  *)bannerView preferredHeight:(CGFloat)preferredHeight{
    NSLog(@"adsAdapterBannerDidLoad:");
    _bannerView = bannerView;
    _bannerView.frame = CGRectMake(0, 20, 320, preferredHeight);
    [self.view addSubview:_bannerView];
}
```
**Swift**

```Swift
  func adsAdapter(_ adsAdapter: MNGAdsAdapter!, bannerDidLoad adView: UIView!, preferredHeight: CGFloat) {
        adView.frame = CGRect(x:0, y:self.view.frame.size.height - 50,width:self.view.frame.size.width,height: 50)
        self.view.addSubview(adView)
    }
```


adsAdapter:bannerDidFailWithError: will be called when all ads servers fail. it will return the error of last called ads server.

**Objective-C**

```objc
-(void)adsAdapter:(MNGAdsAdapter *)adsAdapter bannerDidFailWithError:(NSError *)error{
NSLog(@"%@",error);
}
```
**Swift**

```Swift
  func adsAdapter(_ adsAdapter: MNGAdsAdapter!, bannerDidFailWithError error: Error!) {
        //
    }
```

Some Ad Network (like Smart ads server) allow user to expand and collapse ad.

Even on refresh, banner can change the size.

adsAdapter:bannerDidChangeFrame: will be called when ad did change size

**Objective-C**

```objc

-(void)adsAdapter:(MNGAdsAdapter *)adsAdapter bannerDidChangeFrame:(CGRect)frame{

    ...
}

```
**Swift**

```Swift

  func adsAdapter(_ adsAdapter: MNGAdsAdapter!, bannerDidChangeFrame frame: CGRect) {

    }
```

## Step 3.  Handle callBack from RefreshDelegate
If you want tobe notified on refresh, you have to set refresh delegate

```objc
bannerAdsFactory.refreshDelegate = self;
```
On banner refresh, the SDK invoke the calback

**Objective-C**

```objc
-(void)adsAdapterBannerDidRefresh:(MNGAdsAdapter *)adsAdapter{
    ...
}
```

**Swift**

```swift
 func adsAdapter(_ adsAdapter: MNGAdsAdapter!, adsAdapterBannerDidRefresh) {
        //
    }

```

### MNGAdSize
Mng ads provides variant pre-defined sizes ( example below).

| MNGAdSize | Description |Dimensions 
| --- | --- | --- |
| kMNGAdSizeBanner	| Small Banner	 | 320 x 50 |
| kMNGAdSizeDynamicBanner  | Small Banner Screen |Screen width x 50 |
| kMNGAdSizeLargeBanner   | Large Banner	 |320 x 100 |
| kMNGAdSizeFullBanner |Full Banner ipad| 468 x 60 |
| kMNGAdSizeLeaderboard	| Landscape Banner ipad | 728 x 90|
| kMNGAdSizeDynamicLeaderboard	| Landscape Banner ipad | Screen width x 90 |
| kMNGAdSizeMediumRectangle | Square Banner	 | 300 x 250 |



Example:

```objc
    MNGAdSize size;
    if (isSquare) {
        size = kMNGAdSizeMediumRectangle;
    }else{
        BOOL isIPAD = ([[UIDevice currentDevice] userInterfaceIdiom] == UIUserInterfaceIdiomPad);
        size = (isIPAD)?kMNGAdSizeDynamicLeaderboard:kMNGAdSizeDynamicBanner;
    }
    [bannerAdsFactory loadBannerInFrame:size];
```

### ClickDelegate
The clickDelegate notify you when the ad has been clicked.

**Objective-C**

```objc
//.h
@interface ViewController : UIViewController<MNGClickDelegate>

//.m
adsFactory.clickDelegate = self;

...

-(void)adsAdapterAdWasClicked:(MNGAdsAdapter *)adsAdapter{
    NSLog(@"Ad Clicked");
    ...
}
```
**Swift**

```Swift
class SwiftViewController: UIViewController,MNGClickDelegate,

...
   bannerFactory.clickDelegate = self

   func adsAdapterAdWasClicked(_ adsAdapter: MNGAdsAdapter!) {
        
    }
    
```

### Remove Banner View
f you like to Remove banner from the view, you can use this code :

**Objective-C**

```objc
    [_bannerView removeFromSuperview];
    _bannerView = nil;
    [bannerAdsFactory releaseMemory];
```

**Swift**

``` Swift

    _bannerView.removeFromSuperview()
    _bannerView = nil
    bannerAdsFactory.releaseMemory()

```