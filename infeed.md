![mad_AdNetworkMediation_rgb_small.png](https://bitbucket.org/repo/GyRXRR/images/3981639300-mad_AdNetworkMediation_rgb_small.png) for IOS


# Infeed Integration for IOS
Ads that show up in the middle of the stream as you scroll through your content Parallax or Video.

[TOC]


## Overview
Before You Start. Make sure that you have correctly integrated the MNG SDK into your application. Integration is outlined [here](https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/setup).

## Integration for IOS

## Step 1. Init Infeed factory

To create an **In-Feed** Ad format ( the ads that show up in the middle of the stream as you scroll through your content), you must init an object with type MNGAdsSDKFactory and set the infeedDelegate and the viewController.

**Objective-C**

```objc
infeedAdsFactory = [[MNGAdsSDKFactory alloc]init];
infeedAdsFactory.infeedDelegate = self;
infeedAdsFactory.viewController = self;
```

**Swift**

```swift
    infeedFactory = MNGAdsSDKFactory()
    infeedFactory?.infeedDelegate = self
    infeedFactory?.viewController = self
```
You have also to set placementId (minimum one time)

**Objective-C**

```objc
infeedAdsFactory.placementId = @"/YOUR_APP_ID/PLACEMENT_ID";

```
**Swift**

```swift
  infeedFactory?.placementId = "/YOUR_APP_ID/PLACEMENT_ID"

```
## Step 2. Make a request
To make a request you have to call 'loadInfeedInFrame'. 

###### Parameter :

 - madvertiseFrame: MAdvertiseInfeedFrame  frame with parametres  WidthDP : widht of viewInfeed and infeedRatio:

(INFEED_RATIO_16_9 / INFEED_RATIO_4_3) 

 
  - Returns: void result will be returned in the callback.

  
**Objective-C**
 
```objc
 
   MAdvertiseInfeedFrame * frameinfeed = [[MAdvertiseInfeedFrame alloc] initWithWidthDP:self.view.frame.size.width andInfeedRatio:INFEED_RATIO_16_9];
    [infeedAdsFactory loadInfeedInFrame:frameinfeed withPreferences:preferences ];
```
**Swift**

 
```Swift
 
    let infeedFrame = MAdvertiseInfeedFrame(widthDP: self.view.frame.size.width, andInfeedRatio:INFEED_RATIO_16_9)
   infeedFactory?.loadInfeed(in: infeedFrame, withPreferences: nil)
   
```


## Step 3. Handle callBack from InfeedDelegate
adsAdapter:infeedDidLoad: will be called by the SDK when your bannerView is ready. now you can add your bannerView to th ViewHierarchy.

**Objective-C**

```objc
-(void)adsAdapter:(MNGAdsAdapter  *)adsAdapter infeedDidLoad:(UIView  *)bannerView{
    NSLog(@"adsAdapterInfeedDidLoad:");
    [self.view addSubview:_bannerView];
}
```

**Swift**

```Swift
 func adsAdapter(_ adsAdapter: MNGAdsAdapter!, infeedDidLoad adView: UIView!) {
          print("infeed loaded")
    
    }
```

`NB:` infeed does not return preferredHeight like banner because infeed height depends of width so you can use one the standard ration:

- 5:3 (called also 15:9) : the one used in our demo
- 16:9 : is the international standard format of HDTV


**Objective-C**

```objc
- (CGFloat)tableView:(UITableView *)tableView heightForRowAtIndexPath:(NSIndexPath *)indexPath{
    if (indexPath.row == INFEED_ROW) {
        if (_infeedView) {
            return self.view.frame.size.width * (3./5.);
        }
        return 0;
    }else{
        return OTHER_CELL_ROW_HEIGHT;
    }
}
```

**Swift**

```Swift
func tableView(_ tableView: UITableView, heightForRowAt indexPath: IndexPath) -> CGFloat {
        if indexPath.row == 6 {
            if infeedView != nil {
                return infeedView!.frame.size.height
            }else {
                return 0
            }
            
        }else {
            return 60
        }
    }
```

adsAdapter:infeedDidFailWithError: will be called when all ads servers fail. it will return the error of last called ads server.

**Objective-C**

```objc
-(void)adsAdapter:(MNGAdsAdapter *)adsAdapter infeedDidFailWithError:(NSError *)error{
NSLog(@"%@",error);
}
```

**Swift**

```Swift
 func adsAdapter(_ adsAdapter: MNGAdsAdapter!, infeedDidFailWithError error: Error!) {
        print(error as Any)
        
    }
```
## Step 4. Handle callBack from RefreshDelegate
If you want tobe notified on refresh, you have to set refresh delegate (same as banner)

**Objective-C**

```objc
infeedAdsFactory.refreshDelegate = self;
```
**Swift**

```Swift
infeedFactory?.refreshDelegate = self;
```

### ClickDelegate
The clickDelegate notify you when the ad has been clicked.
**Objective-C**

```objc
//.h
@interface ViewController : UIViewController<MNGClickDelegate>

//.m
adsFactory.clickDelegate = self;

// Objc
-(void)adsAdapterAdWasClicked:(MNGAdsAdapter *)adsAdapter{
    NSLog(@"Ad Clicked");
    ...
}

```

**Swift**

```Swift

//.Swift 
class SwiftViewController: UIViewController,MNGAdsAdapterInfeedDelegate,MNGClickDelegate
...


// Swift
 func adsAdapterAdWasClicked(_ adsAdapter: MNGAdsAdapter!) {
        
    }
    
```
