![mad_AdNetworkMediation_rgb_small.png](https://bitbucket.org/repo/GyRXRR/images/3981639300-mad_AdNetworkMediation_rgb_small.png) for IOS

# Native ads
[TOC]

MNG Ads supports native ads, that allow you to retrieve the metadata of ad campaigns and present the ads yourself, within the context of your app, using your own art style. You are fully responsible
for rendering the ad views using the information we supply. Native ads however offer methods to help you register impressions and clicks on your custom view.

## Overview
Before You Start. Make sure that you have correctly integrated the MNG SDK into your application. Integration is outlined [here](https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/setup).
## 1. Requesting a native ad

##### Import the necessary classes

Objc : 

```objc
#import "MNGNAtiveObject.h"
#import "MNGAdsSDKFactory.h"

```
Swift  : 

You have to import MNGAds SDK's headers in your Bridging-Header.h

```swift
#import "MNGNAtiveObject.h"
#import "MNGAdsSDKFactory.h"

```
##### Init factory

To create a nativeAd  you have to init an object with type MNGAdsSDKFactory and set the nativeDelegate.

Objc : 

```objc
nativeAdsFactory = [[MNGAdsSDKFactory alloc]init];
nativeAdsFactory.nativeDelegate = self;
```
Swift  : 

```swift
 nativeAdFactory = MNGAdsSDKFactory()
 nativeAdFactory.nativeDelegate = self

```
You have also to set placementId (minimum one time)


Objc : 

```objc
nativeAdsFactory.placementId = @"/YOUR_APP_ID/PLACEMENT_ID";
```

Swift  : 

```swift
  nativeAdFactory.placementId = "/YOUR_APP_ID/PLACEMENT_ID"
```
##### Make a request for native ad
Using MNGPreference you can set the preferred adchoices position , although you need to keep in mind that in some cases it might not position it where mentioned since some of the adnetworks wont take this parameter into consideration , so preferably set the preferred position here as well in the didLoad once the request succeeds.

###### Native Ad AdChoice  : 

Finally to execute the request you have to call '[loadNativeWithPreferences]'.

default is loaded with Cover Image


Objc : 

```objc
MNGPreference *preferences = MNGPreference *preferences = [[MNGPreference alloc]init];
[nativeAdsFactory loadNativeWithPreferences:preferences];
```


Swift  : 

```swift
 let preferences = MNGPreference.init()
  nativeAdFactory.loadNative(withPreferences: preferences)
  
```

###### Native Ad AdChoice Without Cover Image
if you like to execute the request  without cover Image you can set the option **withCover**  to NO : 

Objc : 

```objc
MNGPreference *preferences = MNGPreference *preferences = [[MNGPreference alloc]init];
[nativeAdsFactory loadNativeWithPreferences:preferences withCover:NO];

```

Swift  : 

```swift
let preferences = MNGPreference.init()
        nativeAdFactory.loadNative(withPreferences: preferences,withCover:false)
  
```

##### Handle callBack from NativeDelegate
adsAdapter:nativeObjectDidLoad: will be called by the SDK when your nativeObject is ready. now you can create your own view.


Objc : 

```objc
-(void)adsAdapter:(MNGAdsAdapter *)adsAdapter nativeObjectDidLoad:(MNGNAtiveObject *)nativeObject{
NSLog(@"adsAdapterNativeObjectDidLoad:");
self.titleLabel.text = nativeObject.title;
self.contextLabel.text = nativeObject.socialContext;
self.bodyLabel.text = nativeObject.body;
//possibility to customize the badge title
[nativeObject updateBadgeTitle:@"Publicit??"];
badgeView = nativeObject.badgeView;
[_nativeObject registerViewForInteraction:self.nativeView withMediaView:self.backgroundImage withIconImageView:self.iconeImage withViewController:[APP_DELEGATE drawerViewController] withClickableView:self.callToActionButton];
...
}
```


Swift  : 

```swift
func adsAdapter(_ adsAdapter: MNGAdsAdapter!, nativeObjectDidLoad nativeObject: MNGNAtiveObject!) {
        nativeView.layer.borderWidth = 1
        nativeView.layer.borderColor = UIColor.lightGray.cgColor
        titleLabel.text = nativeObject.title
        socialContextLabel.text = nativeObject.socialContext
        descriptionLabel.text = nativeObject.body
        if self.badgeView != nil {
            self.badgeView?.removeFromSuperview()
        }
        self.nativeObject = nativeObject
        badgeView = self.nativeObject?.badgeView
        if (badgeView != nil) {
            var frame = badgeView?.frame
            frame?.origin.y = 3
            frame?.origin.x = 3
            badgeView?.frame = frame!
            self.nativeView.addSubview(badgeView!)
        }
        
        if adChoiceBadgeView != nil {
            adChoiceBadgeView?.removeFromSuperview()
        }
        adChoiceBadgeView = self.nativeObject?.adChoiceBadgeView
        if adChoiceBadgeView != nil {
            var frame = adChoiceBadgeView?.frame
            let widhtFrame = frame!.size.width - 3
            frame?.origin.y = 3
            frame?.origin.x = self.nativeView.frame.size.width - widhtFrame
            adChoiceBadgeView?.frame = frame!
            self.nativeView.addSubview(adChoiceBadgeView!)
        }
        
        // download images
        self.backgroundImage.image = nil
        self.iconeImage.image = nil
        self.iconeImage.layer.cornerRadius = 16
        self.iconeImage.clipsToBounds = true
   
        
        self.callToActionButton.setTitle(self.nativeObject?.callToAction, for: UIControl.State())
        if self.nativeObject?.displayType == MNGDisplayType.appInstall {
            self.callToActionButton.setImage(#imageLiteral(resourceName: "download"), for: UIControl.State())
        }else if self.nativeObject?.displayType == .content {
            self.callToActionButton.setImage(#imageLiteral(resourceName: "arrow"), for: UIControl.State())
        }
        self.callToActionButton.titleLabel?.textAlignment = .center
        
        self.nativeObject?.registerView(forInteraction: self.nativeView, withMediaView: self.backgroundImage, withIconImageView: self.iconeImage, with: self, withClickableView: self.callToActionButton)
        
        self.nativeView.isHidden = false


    }```
    
    
[adsAdapter:nativeObjectDidFail:] will be called when all ads servers fail. it will return the error of last called ads server.

Objc : 

```objc
-(void)adsAdapter:(MNGAdsAdapter *)adsAdapter nativeObjectDidFailWithError:(NSError *)error withCover:(BOOL)cover;
}
```

Swift  : 

```swift
 func adsAdapter(_ adsAdapter: MNGAdsAdapter!, nativeObjectDidFailWithError error: Error!, withCover cover: Bool){
        NSLog("\(String(describing: error))")
    }
    
```

## 2. Native Ad Assets

Once a native ad is loaded, you may retrieve its metadata with the following methods:

### **Ad Title**

 - 50 maximum character length string of ad headline
 - Provide enough space to display the entire length of the Ad Title
 - asset name : **nativeObject.title**


### **Ad Text**

 - 150 maximum character length string of ad text
 - Provide enough space to display the entire length of the Ad Text
 - asset name : **nativeObject.body**

### **CTA Text**

 - Text for a button
 - 12 characters maximum
 - asset name : **nativeObject.callToAction**


### **Sponsored Marker**

 - Badge view (an icon)
 - change according ad network
 - must be inserted on top right
 - asset name : **nativeObject.adChoiceBadgeView**

### **Distinguishable Ad**

 - ???Ad??? (can be localized)
 - Badge that says ???AD??? and is at least 15x15px (can be localized)
 - change according ad network
 - must be inserted on top left
 - asset name : **ativeObject.badgeView**


Objc : 

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


Swift  : 

```swift
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

self.nativeObject?.registerView(forInteraction: self.nativeView, withMediaView: self.backgroundImage, withIconImageView: self.iconeImage, with: self, withClickableView: self.callToActionButton)   
 
```

## 3. Native Ad Implementation

![nativeAd.png](https://bitbucket.org/repo/aen579/images/1993529083-nativeAd.png)

## 4. cache

Ad metadata that you receive can be cached and re-used for up to 3 hours. If you plan to use the metadata after this time period, make a call to load a new ad.


## 5. Assets download

we provide method to download assets.

### ** registerViewForInteraction Param??tres **

    * self.nativeView.   : containerView of native Ad
    * withMediaView      : coverImageView 
    * withIconImageView  : iconeImageView
    * withViewController : parent ViewController of nativeAd
    * withClickableView  : the button of nativeAd 


### **Native Ad Without Cover Image **
Objc:

```objc

[_nativeObject registerViewForInteraction:self.nativeView withMediaView:nil withIconImageView:self.iconeImage withViewController:[APP_DELEGATE drawerViewController] withClickableView:self.callToActionButton];

```
Swift:

```Swift

self.nativeObject?.registerView(forInteraction: self.nativeView, withMediaView: nil, withIconImageView: self.iconeImage, with: self, withClickableView: self.callToActionButton)
        

```
### **Native Ad With Cover Image **

Objc:

```objc

[_nativeObject registerViewForInteraction:self.nativeView withMediaView:self.backgroundImage withIconImageView:self.iconeImage withViewController:[APP_DELEGATE drawerViewController] withClickableView:self.callToActionButton];

```

Swift:

```Swift

self.nativeObject?.registerView(forInteraction: self.nativeView, withMediaView: self.backgroundImage, withIconImageView: self.iconeImage, with: self, withClickableView: self.callToActionButton)
        

```
## 6. customizable Badge

badge in the nativeAd is customizable now using the method:



Objc:

```objc

 [_nativeObject updateBadgeTitle:@"newBadgeTitle"];

```

Swift:

```Swift

 self.nativeObject?.updateBadgeTitle("newBadgeTitle")

```
>note that the new method returns a BOOL indicating if the update was successful or not.

## 7. click - registerViewForInteraction

It's **HIGHLY** recommended to only register ONE and ONLY one view for interaction , because some of the AdNetworks only accept one view and if you try to assign more than one then probably none of the views you assign will be responsive.

## 8. Native Ad Collection  Implementation :


 Check [Carrousel](https://bitbucket.org/mngcorp/mngads-demo-ios/src/master/Demo/MNG-Ads-SDK/CarrouselViewController.m) Page in demo
 
 if you want to get the clicked native Ad from the collection : 

 * set the MNGClickDelegate.

 ```
   //.h

 @interface ViewController : UIViewController<MNGClickDelegate>
 
 
  //.Swift
 SwiftViewController: UIViewController, MNGAdsAdapterNativeDelegate,MNGClickDelegate

 ```

 ```
 nativeCollectionAdsFactory.clickDelegate = self;
 
 ```

 * Handle callBack from MNGClickDelegate
adsAdapterNativeAdWasClicked:nativeObjectClicked: will be called by the SDK when the nativeAd has been clicked  from the collection 

```
-(void)adsAdapterNativeAdWasClicked:(MNGAdsAdapter *)adsAdapter nativeObjectClicked:(MNGNAtiveObject *)clickedAdView{
   
}

//swift 
func adsAdapterNativeAdWasClicked(_ adsAdapter: MNGAdsAdapter!,_ clickedAdView: MNGNAtiveObject!) {
        
    }
```