![mad_AdNetworkMediation_rgb_small.png](https://bitbucket.org/repo/GyRXRR/images/3981639300-mad_AdNetworkMediation_rgb_small.png) for IOS


# Infeed Integration for IOS
Ads that show up in the middle of the stream as you scroll through your content Parallax or Video.

[TOC]


## Overview
Before You Start. Make sure that you have correctly integrated the MNG SDK into your application. Integration is outlined [here](https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/setup).

## Integration for IOS

## Step 1. Init Infeed factory

To create an **In-Feed** Ad format ( the ads that show up in the middle of the stream as you scroll through your content), you must init an object with type MNGAdsSDKFactory and set the infeedDelegate and the viewController.

```objc
infeedAdsFactory = [[MNGAdsSDKFactory alloc]init];
infeedAdsFactory.infeedDelegate = self;
infeedAdsFactory.viewController = self;
```
You have also to set placementId (minimum one time)

```objc
infeedAdsFactory.placementId = @"/YOUR_APP_ID/PLACEMENT_ID";
```
## Step 2. Make a request
To make a request you have to call 'loadInfeedInFrame'. 

###### Parameter :

 - madvertiseFrame: MAdvertiseInfeedFrame  frame with parametres  WidthDP : widht of viewInfeed and infeedRatio:
 
 ```objc
 (INFEED_RATIO_16_9 / INFEED_RATIO_4_3)
 ```

 - Returns: void result will be returned in the callback.

```objc
MAdvertiseInfeedFrame * frameinfeed = [[MAdvertiseInfeedFrame alloc] initWithWidthDP:self.view.frame.size.width andInfeedRatio:INFEED_RATIO_4_3];
[infeedAdsFactory loadInfeedInFrame:frameinfeed withPreferences:preferences];
```

## Step 3. Handle callBack from InfeedDelegate
adsAdapter:infeedDidLoad: will be called by the SDK when your bannerView is ready. now you can add your bannerView to th ViewHierarchy.

```objc
-(void)adsAdapter:(MNGAdsAdapter  *)adsAdapter infeedDidLoad:(UIView  *)bannerView{
    NSLog(@"adsAdapterInfeedDidLoad:");
    [self.view addSubview:_bannerView];
}
```

`NB:` infeed does not return preferredHeight like banner because infeed height depends of width so you can use one the standard ration:

- 5:3 (called also 15:9) : the one used in our demo
- 16:9 : is the international standard format of HDTV

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

adsAdapter:infeedDidFailWithError: will be called when all ads servers fail. it will return the error of last called ads server.

```objc
-(void)adsAdapter:(MNGAdsAdapter *)adsAdapter infeedDidFailWithError:(NSError *)error{
NSLog(@"%@",error);
}
```
## Step 4. Handle callBack from RefreshDelegate
If you want tobe notified on refresh, you have to set refresh delegate (same as banner)

```objc
infeedAdsFactory.refreshDelegate = self;
```


### ClickDelegate
The clickDelegate notify you when the ad has been clicked.

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
