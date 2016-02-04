# Native ads
[TOC]

MNG Ads supports native ads, that allow you to retrieve the metadata of ad campaigns and present the ads yourself, within the context of your app, using your own art style. You are fully responsible
for rendering the ad views using the information we supply. Native ads however offer methods to help you register impressions and clicks on your custom view.

## 1. Requesting a native ad

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
To make a request you have to call '[createNative]'. this method return a bool value (canHandleRequest) 

```objc
if([nativeAdsFactory createNative]){
//Wait callBack from delegate
}else{
//adsFactory can not handle your request
}
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


```objc

// Get the app name
title=nativeObject.title;

// Get the app description (tagline)
body=nativeObject.body;

// Get the app social context
socialContext=nativeObject.socialContext;

// Get the "Ad" badge view. You must show this bitmap on your ad view to denote an ad
badge=nativeObject.badgeView;

// Check whether the app PriceType MNGPriceTypeFree,MNGPriceTypePayable or MNGPriceTypeUnknown
pricetype=nativeObject.priceType

// Get the app purchase price
price=nativeObject.localizedPrice;

// Get the localized text to print on the call to action button, such as "DOWNLOAD , LEARNE MORE ..."
callToAction=nativeObject.callToAction;

// Get the URL of the icon image for the app
 iconUrl=nativeObject.photoUrl;

// Get ahe URL of the cover image for the app
 coverImageUrl=nativeObject.coverImageUrl;

// Register your custom ad view to automatically report impressions and clicks, and react to clicks by opening the app in the store. This is mandatory
[_nativeObject registerViewForInteraction:container withViewController:vc withClickableView:self.callToActionButton];
```
## 3. Native Ad Implementation




## 4. v2.0 or above
You can also integrate video ads into your Native Ad experience. To enable video you must complete the following steps:
 - Have SDK version 2.0 or later
 -  You have to call [setMediaContainer:(UIView*)] then the sdk will handle the rendering process ( displaying)  the image cover or the media video inside the view group that depends on the ad network result
```objc
[nativeObject setMediaContainer:self.container];
```

![Capture d’écran 2016-02-04 à 12.46.24 PM.png](https://bitbucket.org/repo/aen579/images/2619653194-Capture%20d%E2%80%99e%CC%81cran%202016-02-04%20a%CC%80%2012.46.24%20PM.png)