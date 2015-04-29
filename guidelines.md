# Best practice Mngads : optimized use case for several ad formats on one page

When trying to display several ad formats on one page try to synchronize your requests instead of making multiple ones at the some time. By making the requests at the same time you are decreasing your chance of receving an Ad and you are making your app slow .You can check the number of MNGAdsFactory running a request by calling or use delegate like [FourInOneViewController.m](https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/FourInOneViewController.m?at=master) :

```objc
if([MNGAdsSDKFactory numberOfRunningFactory] <= MAX_ALLOWED_FACTORIES){
	//send your request
}
```

# Design Guidelines for MNG Ads

## Banner

A banner is a small bar ad that appears at the bottom or top of your content. Usually sized 320 x 50. Only include one ad per page or show one ad at a time if scrolling.

## Square

## Interstitial

An interstitial is a full screen ad that appears at a natural transition point in your app.

## Native Ad

A native ad is a custom designed ad that fits seamlessly with your app. If done well, ads can blend in naturally with your interface.