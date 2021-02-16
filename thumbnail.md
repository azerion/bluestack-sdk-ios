# Thumbnail Ad Integration for IOS

[TOC]

## Overview
Before You Start. Make sure that you have correctly integrated the MNG SDK into your application. Integration is outlined [here](https://bitbucket.org/mngcorp/mobile.mng-ads.com-mngperf/wiki/setup).


## Step 1. Init Thumbnail Factory

To create an Thumbnail Ad format ( the ads that show up in the middle of the stream as you scroll through your content), you must init an object with type MNGAdsSDKFactory and set the thumbnailAdDelegate and the viewController.

**Objective-C**

```ObjectiveC
MNGAdsSDKFactory * thumbnailadsFactory = [[MNGAdsSDKFactory alloc]init];
```
**Swift**

```Swift
let thumbnailadsFactory: MNGAdsSDKFactory! = MNGAdsSDKFactory()
```

## Step 2. Set Placement ID

You have also to set placement Id :

**Objective-C**

```ObjectiveC
    thumbnailadsFactory.placementId = @"/YOUR_APP_ID/PLACEMENT_ID";
```
**Swift**

```Swift
        thumbnailadsFactory.placementId = "/YOUR_APP_ID/PLACEMENT_ID"
```

## Step 3. Handle callBack from BluestackThumbnailAdDelegate
Next, implement the BluestackThumbnailAdDelegate in your code. 

**Objective-C**

```ObjectiveC
    thumbnailadsFactory.thumbnailAdDelegate = self;
```
**Swift**

```Swift
    thumbnailadsFactory.thumbnailAdDelegate = self;
```

The SDK will notify your delegate of all possible events listed below :

- adsAdapterThumbnailAdAdLoaded: will be called by the SDK when your ThumbnailAd is ready to showing. now you can show your ThumbnailAd.

**Objective-C**

```ObjectiveC
#pragma mark - Thumbnail Delegate
-(void)adsAdapterThumbnailAdAdLoaded:(MNGAdsAdapter *)adsAdapter{
    if (isCustom) {
        MNGPreference *preferences = [Utils getTestPreferences];
        preferences.preferredThumbnailAdChoicePosition = BlueStackAdChoiceTopLeft;
        [thumbnailadsFactory showThumbnailInGravity:preferences inXMargin:120 inyMargin:120];
    }else{
        [thumbnailadsFactory showThumbnail];
    }
   
}
```

**Swift**

```Swift
func adsAdapterThumbnailAdAdLoaded(_ adsAdapter: MNGAdsAdapter!) {

 if (isCustom) {
        let preferences = Utils.getTestPreferences()
        preferences.preferredThumbnailAdChoicePosition = BlueStackAdChoiceTopLeft;
        thumbnailadsFactory.showThumbnailInGravity:preferences inXMargin:120 inyMargin:120];
                thumbnailadsFactory.showThumbnailInGravity(inGravity: preferences, inXMargin: 120, inyMargin: 120)

    }else{
        [thumbnailadsFactory showThumbnail];
    }
}    
```

- adsAdapterThumbnailAdAdError:withError:error: will be called when all ads servers fail. it will return the error of last called ads server.

**Objective-C**

```ObjectiveC
-(void)adsAdapterThumbnailAdAdError:(MNGAdsAdapter *)adsAdapter withError:(NSError *)error{
    
}
```

**Swift**

```Swift
func adsAdapterThumbnailAdAdError(_ adsAdapter: MNGAdsAdapter!, withError error: Error!) {
        
    }
```
- adsAdapterThumbnailAdAdClosed(): will be called when Thumbnail Ads closed by the user. 

**Objective-C**

```ObjectiveC
-(void)adsAdapterThumbnailAdAdClosed:(MNGAdsAdapter *)adsAdapter{
    
}

```

**Swift**

```Swift
func adsAdapterThumbnailAdAdClosed(_ adsAdapter: MNGAdsAdapter!) {
        
    }
    
```

- adsAdapterThumbnailAdAdDisplayed(): will be called when Thumbnail Ads has been displayed on the screen.

**Objective-C**

```ObjectiveC
-(void)adsAdapterThumbnailAdAdDisplayed:(MNGAdsAdapter *)adsAdapter{
    
}

```

**Swift**

```Swift
func adsAdapterThumbnailAdAdDisplayed(_ adsAdapter: MNGAdsAdapter!) {
        
    }
    
```


## Step 4. Load a Thumbnail Ad

To start loading an ad, call the load method:

```java
mthumbnailAdsFactory.loadThumbnail()
```

## Step 5. Show a Thumbnail Ad

To display the ad, call the showThumbnail method:


**Objective-C**

```ObjectiveC
[thumbnailadsFactory showThumbnail];

```

**Swift**

```Swift
thumbnailadsFactory.showThumbnail
    
```

## Troubleshooting
 
### Customize Thumbnail Ad size

In order to control the thumbnail size, call load method with maxWidth and maxHeight (Both values are in px) parameters:
**Objective-C**

```ObjectiveC
    [thumbnailadsFactory loadThumbnailAdInMaxWidth:300 withMaxHeight:300 withPreferences:preferences];

```

**Swift**

```Swift
thumbnailadsFactory.loadThumbnailAd(inMaxWidth: 300, withMaxHeight: 300, withPreferences: preferencess)

    
```

The following constraints apply on the values you can pass to these parameters:

- maxWidth and maxHeight must not be greater than the size of the screen.
- maxWidth and maxHeight must be greater than or equal to 101px.
- longest side, either maxWidth or maxHeight, must be greater than or equal to
 180px.


### Check if a Thumbnail Ad is loaded

Call the following method to check if a Thumbnail Ad is ready to be displayed:

**Objective-C**

```ObjectiveC
    [thumbnailadsFactory isThumbnailReady()];

```

**Swift**

```Swift
thumbnailadsFactory.isThumbnailReady()

```

### Set Thumbnail Ad position

To set the thumbnail position, call the show Thumbnail method with gravity and margin parameters:

**Objective-C**

```ObjectiveC
MNGPreference *preferences = [Utils getTestPreferences];
        preferences.preferredThumbnailAdChoicePosition = BlueStackAdChoiceTopLeft;
        [thumbnailadsFactory showThumbnailInGravity:preferences inXMargin:120 inyMargin:120];
        
```

**Swift**

```Swift
thumbnailadsFactory.showThumbnail(inGravity: preferences, inXMargin: 300, inyMargin: 300)

```


The show method takes the following parameters:

- gravity : the corner based on which the thumbnail will be positioned and 
MNGPreference *preferences ;
preferences.preferredThumbnailAdChoicePosition = 
it can have the following values:
	- BlueStackAdChoiceTopLeft
	- BlueStackAdChoiceTopRight
	- BlueStackAdChoiceTopLeft
	- BlueStackAdChoiceBottomRight
- xMargin: distance on the x axis from the gravity corner to thumbnail. Value must be in px.
- yMargin: distance on the y axis from the gravity corner to thumbnail. Value must be in px.