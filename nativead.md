# Native ads
[TOC]

MNG Ads supports native ads, that allow you to retrieve the metadata of ad campaigns and present the ads yourself, within the context of your app, using your own art style. You are fully responsible
for rendering the ad views using the information we supply. Native ads however offer methods to help you register impressions and clicks on your custom view.

## 1. Requesting a native ad

##### Import the necessary classes

```objc
#import "MNGNAtiveObject.h"
#import "MNGAdsSDKFactory.h"
```

##### Init factory

To create a nativeAd  you have to init an object with type MNGAdsSDKFactory and set the nativeDelegate.

```objc
nativeAdsFactory = [[MNGAdsSDKFactory alloc]init];
nativeAdsFactory.nativeDelegate = self;
```
You have also to set placementId (minimum one time)

```objc
nativeAdsFactory.placementId = @"/YOUR_APP_ID/PLACEMENT_ID";
```
##### Make a request for native ad
Using MNGPreference you can set the preferred adchoices position , although you need to keep in mind that in some cases it might not position it where mentioned since some of the adnetworks wont take this parameter into consideration , so preferably set the preferred position here as well in the didLoad once the request succeeds.

###### Native Ad AdChoice

Finally to execute the request you have to call '[loadNativeWithPreferences]'.

```objc
MNGPreference *preferences = MNGPreference *preferences = [[MNGPreference alloc]init];
preferences.preferredAdChoicesPosition = MAdvertiseAdChoiceTopLeft;
[nativeAdsFactory loadNativeWithPreferences:preferences];
```

##### Handle callBack from NativeDelegate
[adsAdapter:nativeObjectDidLoad:] will be called by the SDK when your nativeObject is ready. now you can create your own view.
```objc
-(void)adsAdapter:(MNGAdsAdapter *)adsAdapter nativeObjectDidLoad:(MNGNAtiveObject *)nativeObject{
NSLog(@"adsAdapterNativeObjectDidLoad:");
self.titleLabel.text = nativeObject.title;
self.contextLabel.text = nativeObject.socialContext;
self.bodyLabel.text = nativeObject.body;
[nativeObject setMediaContainer:self.container];
...
}
```

[adsAdapter:nativeObjectDidFail:] will be called when all ads servers fail. it will return the error of last called ads server.
```objc
-(void)adsAdapter:(MNGAdsAdapter *)adsAdapter nativeObjectDidFailWithError:(NSError *)error{
NSLog(@"%@",error);
}
```

##2. Native Ad Assets

Once a native ad is loaded, you may retrieve its metadata with the following methods:

###**Main Image**

 - 1200x627px image,
 - Wide aspect ratio main image.
 - asset name : **nativeObject.coverImageUrl**


###**Icon Image**

 - 128x128 max
 - asset name : **nativeObject.photoUrl**


###**Ad Title**

 - 50 maximum character length string of ad headline
 - Provide enough space to display the entire length of the Ad Title
 - asset name : **nativeObject.title**


###**Ad Text**

 - 150 maximum character length string of ad text
 - Provide enough space to display the entire length of the Ad Text
 - asset name : **nativeObject.body**

###**CTA Text**

 - Text for a button
 - 12 characters maximum
 - asset name : **nativeObject.callToAction**


###**Sponsored Marker**

 - Badge view (an icon)
 - change according ad network
 - must be inserted on top right
 - asset name : **nativeObject.adChoiceBadgeView**

###**Distinguishable Ad**

 - “Ad” (can be localized)
 - Badge that says “AD” and is at least 15x15px (can be localized)
 - change according ad network
 - must be inserted on top left
 - asset name : **ativeObject.badgeView**

```objc

// Get the app name
title=nativeObject.title;

// Get the app description (tagline)
body=nativeObject.body;

// Get the "Ad" badge view. You must show this view on your ad view to denote an ad
if(nativeObject.badgeView){
	badge=nativeObject.badgeView;
	...
}

// Get the "AdChoice" badge view. You must show this view on your ad view to denote an ad
if(nativeObject.adChoiceBadgeView){
	adChoiceBadge=nativeObject.adChoiceBadgeView;
	...
}

// Get the localized text to print on the call to action button, such as "DOWNLOAD , LEARNE MORE ..."
callToAction=nativeObject.callToAction;

[_nativeObject registerViewForInteraction:...];

```
###**Native Ad Without Cover Image **
```objc

[_nativeObject registerViewForInteraction:self.nativeView withMediaView:nil withIconImageView:self.iconeImage withViewController:[APP_DELEGATE drawerViewController] withClickableView:self.callToActionButton];

```

###**Native Ad With Cover Image **
```objc

[_nativeObject registerViewForInteraction:self.nativeView withMediaView:self.backgroundImage withIconImageView:self.iconeImage withViewController:[APP_DELEGATE drawerViewController] withClickableView:self.callToActionButton];

```

## 3. Native Ad Implementation

![native-ios.png](https://bitbucket.org/repo/aen579/images/1393323123-native-ios.png)


## 4. Video
You can also integrate video ads into your Native Ad experience. To enable video you must complete the following steps:
 - Have SDK version 2.0 or later
 -  You have to call [setMediaContainer:(UIView*)] then the sdk will handle the rendering process ( displaying)  the image cover or the media video inside the view group that depends on the ad network result
```objc
[nativeObject setMediaContainer:self.container];

```

## 4. cache

Ad metadata that you receive can be cached and re-used for up to 3 hours. If you plan to use the metadata after this time period, make a call to load a new ad.


## 5. Assets download

we provide method to download assets.

```objc
__weak NativeAdViewController *weakSelf = self;
    [nativeObject downloadAssetWithType:MAdvertiseAssetTypeAppIcon completition:^(UIImage *image) {
        dispatch_async(dispatch_get_main_queue(), ^{
            if (!weakSelf) {
                return;
            }
            __strong NativeAdViewController *strongSelf = weakSelf;
            strongSelf.iconeImage.image = image;
            strongSelf.nativeView.hidden = NO;
        });
    }];
```

## 6. customizable Badge

badge in the nativeAd is customizable now using the method:

```
    [_nativeObject updateBadgeTitle:@"newBadgeTitle"];

```

>note that the new method returns a BOOL indicating if the update was successful or not.

## 7. click - registerViewForInteraction

It's **HIGHLY** recommended to only register ONE and ONLY one view for interaction , because some of the AdNetworks only accept one view and if you try to assign more than one then probably none of the views you assign will be responsive.