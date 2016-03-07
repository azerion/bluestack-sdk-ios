# ![MNG-Ads-1.png](https://bitbucket.org/repo/aen579/images/3739691856-MNG-Ads-1.png) for IOS

Thanks for taking a look at mngAds! We take pride in having an easy-to-use, flexible monetization solution.

## Need Help?

You can find integration documentation on our [wiki] and additional help documentation on our [developer help site].

##Using CocoaPods
The MngAds SDK is available through [Cocoapods], a popular dependency management system for Objective-C projects.

To download and incorporate the MngAds SDK into your project using Cocoapods, add the following line to your project's podfile:

```ruby
pod "MNGAds/MNGAdsFull"
```
MngAds maintains adapters for several third party networks. A number of them are available through our Cocoapod spec that provides a simple integration experience. However, following libs/frameworks ** do not yet own a pod. Therefore, you must add these libs/frameworks  manually to your project**

  - [libSmartAdServer.a]
  - [AmazonAd.framework]
  - [LiveRailSDK.framework]

After running `pod install` (if you’re setting up Cocoapods for the first time) or `pod update` (if you’re adding MNGAds to an existing Cocoapods project), it will be ready to use the base MngAds SDK. » 


### Troubleshooting

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

#### cherry-pick install

To add specifics adNetwork.

```ruby
pod "MNGAds" //to add Only MNG ADSERVER
pod "MNGAds/Facebook" // to add Facebook Audience Network
pod "MNGAds/DFP" // to add DFP
pod "MNGAds/SmartAdsServer" // to add SAS
pod "MNGAds/LiveRail" // to add LiveRail
pod "MNGAds/Amazon" // to add Amazon
pod "MNGAds/Flurry" // to add Flurry

```
[wiki]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Home
[developer help site]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/faq
[Cocoapods]:http://cocoapods.org/
[libSmartAdServer.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/sdk/libSmartAdServer.a?at=master&fileviewer=file-view-default
[FBAudienceNetwork.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/FBAudienceNetwork.framework/?at=master
[libANSDK.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/ANSDK/?at=master
[LiveRailSDK.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/LiveRailSDK.framework/?at=master
[AmazonAd.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/AmazonAd.framework/?at=master