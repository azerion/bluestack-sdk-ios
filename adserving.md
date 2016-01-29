![MNG-Ads-1.png](https://bitbucket.org/repo/aen579/images/3739691856-MNG-Ads-1.png) iOS for
![4193248577-af.png](https://bitbucket.org/repo/aen579/images/2031262448-4193248577-af.png) only


[TOC]

MNG Ads can be used for appsfire nativeAds only.

 - http://appsfire.com/
## Start Integrating MNGAds Server

### Banner

```
...
#import "MNGBannerView.h"
...

// init banner view
banner = [[MNGBannerView alloc]initWithFrame:CGRectMake(0, 0, SCREEN_WIDTH, 50)];
    banner.publisherId = @"YOUR_PUBLISHER_ID";
    banner.age = @"29";
    banner.adSize = kMNGAdServerSizeBanner50;
    banner.delegate = self;
    banner.viewController = self;
    
```
##### Ad size MNGAdSize
```
extern CGSize const kMNGAdServerSizeBanner50; //Small Banner screenWidth x 50
extern CGSize const kMNGAdServerSizeLargeBanner100; //Large Banner screenWidth x 100
extern CGSize const kMNGAdServerSizeFullBanner60; //Full Banner ipad screenWidth x 60
extern CGSize const kMNGAdServerSizeLeaderboard90; //Landscape Banner ipad screenWidth x 90
extern CGSize const kMNGAdServerSizeMediumRectangle; //Square Banner 300 x 250

```

##### Make a request
To make a request you must call loadAd

```
[banner loadAd];
```

##### Handle callBack from MNGBannerViewDelegate
```
-(void)bannerViewDidLoad:(MNGBannerView *)bannerView{
    NSLog(@"bannerView did load");
    [self.container addSubview:bannerView];
}

-(void)bannerView:(MNGBannerView *)bannerView didFailWithError:(NSError *)error{
    NSLog(@"bannerView did fail with error : %@",error);
}

-(void)bannerViewDidClicked:(MNGBannerView *)bannerView{
    NSLog(@"bannerView did clicked");
}
```

### Interstitial

```objc
    ...
    #import "MNGInterstitialViewController.h"
    ...
    // init interstitial
    interstitial = [[MNGInterstitialViewController alloc]init];
    interstitial.publisherId = @"YOUR_PUBLISHER_ID";
    interstitial.age = @"29";
    interstitial.delegate = self;
    interstitial.viewController = self;
    
```
##### Make a request 
To make a request you have to call loadAd 

```
     [interstitial loadAd];
```
##### Handle callBack from MNGInterstitialViewDelegate
```objc
#pragma mark - MNGInterstitialViewDelegate
-(void)intertitialDidLoad:(nonnull MNGInterstitialViewController *)interstitialViewController{
    NSLog(@"intertitial did load");
}

-(void)intertitial:(nonnull MNGInterstitialViewController *)interstitialViewController didFailWithError:(nullable NSError *)error{
    NSLog(@"intertitial did fail with error : %@",error);
    
}
-(void)intertitialWillDisappear:(nonnull MNGInterstitialViewController *)interstitialViewController{
    NSLog(@"intertitial will disappear");
}

-(void)intertitialDidClicked:(MNGInterstitialViewController *)interstitialViewController{
    NSLog(@"intertitial did clicked");
}
```

##### Displaying interstitial
```
if([interstitial isReady]){
    [interstitial present];
}
```
#### Debug Mode

To enable debug mode for interstitials or banners, you must use class method setDebugEnabled.

```objc
    [MNGInterstitialViewController setDebugEnabled:YES];
    [MNGBannerView setDebugEnabled:YES];
```

#### Preferences 
Preferences object is an optional parameter that allow you select ads by user info.
informations that you can set are:

- Age : user age
- Location : user geographical position
- Gender : user gender
- Zip : user zip