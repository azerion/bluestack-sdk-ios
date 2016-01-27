##Using CocoaPods
The MngAds SDK is available through [Cocoapods], a popular dependency management system for Objective-C projects.

To download and incorporate the MngAds SDK into your project using Cocoapods, add the following line to your project's podfile:

- To add all adNetworks
```ruby
pod "MNGAds/MNGAdsFull"
```
- To add specific adNetwork (you can add more than one)
```ruby
pod "MNGAds" //to add Only MNG ADSERVER
pod "MNGAds/Facebook" // to add Facebook Audience Network
pod "MNGAds/DFP" // to add DFP
pod "MNGAds/SmartAdsServer" // to add SAS
pod "MNGAds/LiveRail" // to add LiveRail
pod "MNGAds/Amazon" // to add Amazon
pod "MNGAds/Flurry" // to add Flurry

```
After running pod install (if you’re setting up Cocoapods for the first time) or pod update (if you’re adding MNGAds to an existing Cocoapods project),you must add [libSmartAdServer.a](if you added MNGAdsFull or SmartAdsServer), [AmazonAd.framework](if you added MNGAdsFull or Amazon) and [LiveRailSDK.framework] (if you added MNGAdsFull or LiveRail) manually to your project and it will be ready to use the base MngAds SDK.
###Troubleshooting

 - http://guides.cocoapods.org/using/troubleshooting.html
If you have those build errors: 
```
Library not found for -lMNGAds
Header not found for ...
```

You have to check if:
- Header search paths
- Framework search paths
- Library search paths
- Other linker Flags

contains the value ***$(inherited)***



[Cocoapods]:http://cocoapods.org/
[libSmartAdServer.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/SASsdk/?at=master
[FBAudienceNetwork.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/FBAudienceNetwork.framework/?at=master
[libANSDK.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/ANSDK/?at=master