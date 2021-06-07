![mad_AdNetworkMediation_rgb_small.png](https://bitbucket.org/repo/GyRXRR/images/3981639300-mad_AdNetworkMediation_rgb_small.png) for IOS


# Interstitial Integration for IOS

[TOC]

## Overview
Before You Start. Make sure that you have correctly integrated the MNG SDK into your application. Integration is outlined [here](https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/setup).

## Step 1. Init Interstitial factory


**On info.plist if you are using "View controller-based status bar appearance" (UIViewControllerBasedStatusBarAppearance), it must be setted to YES**


![statusbar.png](https://bitbucket.org/repo/aen579/images/4293410302-statusbar.png)


To create an interstitial you must init an object with type MNGAdsSDKFactory and set the interstitalDelegate and the viewController.

**Objective-C**

```objc
interstitialAdsFactory = [[MNGAdsSDKFactory alloc]init];
interstitialAdsFactory.interstitialDelegate = self;
interstitialAdsFactory.viewController = self;
```

**Swift**

```Swift
interstitialAdsFactory = MNGAdsSDKFactory()
interstitialAdsFactory.interstitialDelegate = self
interstitialAdsFactory.viewController = self

```
## Step 2. Set Placement ID

You have also to set placementId (minimum one time)

**Objective-C**

```objc
interstitialAdsFactory.placementId = @"/YOUR_APP_ID/PLACEMENT_ID";

```

**Swift**

```Swift
interstitialAdsFactory.placementId = "/YOUR_APP_ID/PLACEMENT_ID"

```

## Step 3. Make a request
To make a request you must call 'loadInterstitial'.


**Objective-C**

```objc
[interstitialAdsFactory loadInterstitial];

```

**Swift**

```Swift
  interstitialAdsFactory.loadInterstitial()
        
```
## Step 4. Handle callBack from InterstitialDelegate
adsAdapterInterstitialDidLoad: will be called by the SDK when your Interstitial is ready. Interstitial will be showen.

**Objective-C**

```objc
-(void)adsAdapterInterstitialDidLoad:(MNGAdsAdapter *)adsAdapter{
NSLog(@"adsAdapterInterstitialDidLoad");
...
}
```

**Swift**

```Swift
 func adsAdapterInterstitialDidLoad(_ adsAdapter: MNGAdsAdapter!) {
        NSLog("adsAdapterInterstitialDidLoad")
       ...
    }
        
```
adsAdapter:interstitialDidFailWithError: will be called when all ads servers fail. it will return the error of last called ads server.


**Objective-C**

```objc
-(void)adsAdapter:(MNGAdsAdapter *)adsAdapter interstitialDidFailWithError:(NSError *)error{
NSLog(@"%@",error);
}
```

**Swift**

```Swift
 func adsAdapter(_ adsAdapter: MNGAdsAdapter!, interstitialDidFailWithError error: Error!) {
        NSLog("\(String(describing: error))")
    }
        
```
adsAdapterInterstitialDisappear: will be called when intertisialView did disappear. now you can update your UI for example.


**Objective-C**

```objc
-(void)adsAdapterInterstitialDisappear:(MNGAdsAdapter *)adsAdapter{
NSLog(@"adsAdapterInterstitialDisappear");
//For example
HomeViewController *home =  [[HomeViewController alloc]init];
[self.navigationController pushViewController:home animated:YES];
}
```

**Swift**

```Swift
func adsAdapterInterstitialDisappear(_ adsAdapter: MNGAdsAdapter!) {
        NSLog("adsAdapterInterstitialDisappear")
    }
     
```

## Step 5. Disable auto-displaying
With v2.0.4 you can disable auto-displaying.

**Objective-C**

```objc
[interstitialAdsFactory loadInterstitialWithPreferences:preferences autoDisplayed:NO];
```

**Swift**

```Swift
 let preferencess = MNGPreference.init()
 interstitialAdsFactory.loadInterstitial(withPreferences: preferencess, autoDisplayed: false)
     
```
To show the interstitial after succes you have call [displayInterstitial] that would preset the interstitial using the viewController passed to the factory, if you wish to have more control over the presentation process you could use showAdFromRootViewController.

To check if the interstitial is reday to be showen, you have to call [isInterstitialReady].


**Objective-C**

```objc
if ([interstitialAdsFactory isInterstitialReady]) {
    [interstitialAdsFactory displayInterstitial];
}

// OR
if ([interstitialAdsFactory isInterstitialReady]) {
    [interstitialAdsFactory showAdFromRootViewController:rootViewController animated:YES];
}

```

**Swift**

```Swift

if interstitialAdsFactory.isInterstitialReady() {
            interstitialAdsFactory.displayInterstitial()

        }
 // OR

if interstitialAdsFactory.isInterstitialReady() {
            interstitialAdsFactory.showAd(fromRootViewController:self , animated: true)

        }
     
```



___info:___ in some cases the difference between displayInterstitial and showAdFromRootViewController is a little bigger, for example in the case of smart adserver using displayInterstitial will add the the interstitial as a subview in the view of the viewController assigned to the factory, however when using showAdFromRootViewController it will present the interstitial as a viewController which is the case for most other adservers.


___info:___ To test auto-displayin disabled on demo, you have to go to the page interstitial. others interstitials (return background, when change from page to page...) are with auto-displaying.

### ClickDelegate
The clickDelegate notify you when the ad has been clicked.
**Objective-C**

```objc
//.h
@interface ViewController : UIViewController<MNGClickDelegate>

//.m
adsFactory.clickDelegate = self;


//objc

-(void)adsAdapterAdWasClicked:(MNGAdsAdapter *)adsAdapter{
    NSLog(@"Ad Clicked");
    ...
}
```
**Swift**

```objc
//.Swift
SwiftViewController: UIViewController, MNGAdsAdapterInterstitialDelegate,MNGClickDelegate

...
//swift 
func adsAdapterAdWasClicked(_ adsAdapter: MNGAdsAdapter!) {
        
    }
  

```

If you show an interstitial at the didEnterForeground, you can use click delegate to check up if the application enter background by user or after an ad click.

**Objective-C**

```objc
- (void)applicationDidEnterBackground:(UIApplication *)application {
    if ([self.lastClickDate timeIntervalSinceNow] >= -10.) {
        _isAdClicked = YES;
        NSLog(@"Next enter background will be ignored");
    }

}

- (void)applicationDidBecomeActive:(UIApplication *)application {
    if ([MNGAdsSDKFactory isInitialized] && !_isAdClicked) {
        NSLog(@"applicationDidBecomeActive");
        [self displayInters];
    }
    _isAdClicked = NO;
}

-(void)adsAdapterAdWasClicked:(MNGAdsAdapter *)adsAdapter{
    NSLog(@"Banner clicked");
    [((AppDelegate*)[[UIApplication sharedApplication]delegate])setLastClickDate:[NSDate date]];
}

```

