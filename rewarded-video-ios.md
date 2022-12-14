![mad_AdNetworkMediation_rgb_small.png](https://bitbucket.org/repo/GyRXRR/images/3981639300-mad_AdNetworkMediation_rgb_small.png) for IOS

# MAdvertiseRewardedVideoAd for Ios

[TOC]

**MAdvertiseRewardedVideoAd** that will serve to deliver rewarded video ads which are a full screen experience where users opt-in to view a video ad in exchange for something of value, such as virtual currency, in-app items, exclusive content, and more. The ad experience is 15-30 second non-skippable and contains an end card with a call to action. Upon completion of the full video, you will receive a callback to grant the suggested reward to the user.

## Requirement

Require MngAdsSDK >= 2.8

## Overview
Before You Start. Make sure that you have correctly integrated the MNG SDK into your application. Integration is outlined [here](https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/setup).


## Implementation:

In your View Controller header file, import the 2 Reward Video Ad headers, declare that you implement the MAdvertiseAdapterRewardedVideoAdDelegate protocol and add an instance variable for the rewarded video ad :

```
#!objective-c
#import <UIKit/UIKit.h>
#import "MAdvertiseReward.h"
#import "MAdvertiseRewardedVideoAd.h"

@interface RewardedVideoViewController : UIViewController <MAdvertiseAdapterRewardedVideoAdDelegate>

@end
```

```
#!swift in -Bridging-Header.h
#import <BlueStackSDK/MAdvertiseReward.h>
#import <BlueStackSDK/MAdvertiseRewardedVideoAd.h>

```

```
#!swift 
class RewardVideoViewController: UIViewController, MAdvertiseAdapterRewardedVideoAdDelegate {
   }

```



Add a function in your View Controller that initializes the rewarded video object and caches the video creative ahead of the time you want to show it.

```
#!objective-c
MAdvertiseRewardedVideoAd *rewardedVideoAd;

- (void) viewDidLoad {
  [super viewDidLoad];

  [self loadRewardedVideoAd];
}

- (void) loadRewardedVideoAd
{
  rewardedVideoAd = [[MAdvertiseRewardedVideoAd alloc]initWithPlacementID:@"YOUR_PLACEMENT_ID"];
  [rewardedVideoAd setDelegate:self];
  [rewardedVideoAd loadAd];
  //You can use loadAdWithPreferences: as well for better targeting
}

```
```
#!Swift
var rewardedVideoAd : MAdvertiseRewardedVideoAd?

  override func viewDidLoad() {
        super.viewDidLoad()
        self.loadRewardedVideoAd()

    }

func loadRewardedVideoAd()
{
       rewardedVideoAd = MAdvertiseRewardedVideoAd.init("YOUR_PLACEMENT_ID")
       rewardedVideoAd?.delegate = self
       rewardedVideoAd?.load()

  //You can use loadAdWithPreferences: as well for better targeting
}

```

Now that you have added the code to load the ad, you can add the MAdvertiseAdapterRewardedVideoAdDelegate methods which will handle various events.

For example :

```
#!objective-c
/** Notifies the delegate that the creative from the reward video ad has been loaded.

 @param adsAdapter An  object informing the delegate about the reward video being loaded.

 */

- (void)adsAdapterRewardedVideoAdDidLoad:(MNGAdsAdapter *)adsAdapter;

/** Notifies the delegate that the creative from the reward video ad has been failed.

 @param adsAdapter An object informing the delegate about the reward video being failed.
 @param error describing what went wrong.

 */

- (void)adsAdapter:(MNGAdsAdapter *)adsAdapter rewardedVideoAdDidFailWithError:(NSError *)error;
```


```
#!Swift
func adsAdapterRewardedVideoAdDidLoad(_ adsAdapter: MNGAdsAdapter!) { }
    
    func adsAdapter(_ adsAdapter: MNGAdsAdapter!, rewardedVideoAdDidFailWithError error: Error!) { }
    

    func adsAdapterRewardedVideoAdDidClose(_ adsAdapter: MNGAdsAdapter!) {
        
    }
    
    func adsAdapterRewardedVideoAdDidClick(_ adsAdapter: MNGAdsAdapter!) {
        
    }
    
    func adsAdapterRewardedVideoAdWillLogImpression(_ adsAdapter: MNGAdsAdapter!) {
        
    }
    
```


- Once the Video has been loaded, you will need to present it whenever you see fit using the following method :

```
#!objective-c
-(void)showAdFromRootViewController:(UIViewController*)rootViewController animated:(BOOL)flag;
```

```
#!Swift
rewardedVideoAd?.show(fromRootViewController: self, animated: true)
```


But the most important callBack has to be :

```
#!objective-c

- (void)adsAdapterRewardedVideoAdComplete:(MNGAdsAdapter *)adsAdapter withReward:(MAdvertiseReward *)reward;

```
```
#!Swift

    func adsAdapterRewardedVideoAdComplete(_ adsAdapter: MNGAdsAdapter!, with reward: MAdvertiseReward!) {
        var message = "Video rewarded"
        if (reward != nil) {
            message = "\(message) \ntype:\( reward.type ?? "Not Found") \namount: \(reward.amount ?? 0)"
        }
         
    }

```


which serve to inform the publisher that the user has finished watching the video and should be rewarded with the suggested MAdvertiseReward, which is a new object representing, as the name suggest, the reward and it has 2 main properties: amount and type, for example 100 (amount of the reward) diamonds (type of the reward),
the reward can be set from the web console of the differents adnetworks used , although some of them will return a nil reward, for example ads coming from facebook audience will just inform you that the user finished watching but wont suggest a reward , rather leave it to the publisher to decide the fitting reward on his own, so the publisher should always verify the reward object accordingly.

- Obviously incase of fail, you can always try to load an Interstitial or any other type of ad incase you need to display something to the user, but of course any other type of ad wont invoke reward callback.


# Example

 - [Example Reward Video objective C]
 - [Example Reward Video Swift]


 [Example Reward Video objective C]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/master/Demo/MNG-Ads-SDK/RewardVideoViewController.m
 [Example Reward Video Swift ]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/master/DemoSwift/DemoSwift/RewardVideoViewController.swift