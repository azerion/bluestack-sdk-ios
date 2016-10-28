# ![MNG-Ads-1.png](https://bitbucket.org/repo/aen579/images/3739691856-MNG-Ads-1.png) for IOS

Thanks for taking a look at mngAds! We take pride in having an easy-to-use, flexible monetization solution.

## Need Help?

You can find integration documentation on our [wiki] and additional help documentation on our [developer help site].

##Using CocoaPods
The MngAds SDK is available through [Cocoapods], a popular dependency management system for Objective-C projects.

To download and incorporate the MngAds SDK into your project using Cocoapods, add the following line to your project's podfile:
```ruby
pod "MNGAds"
```
Or:
```ruby
pod "MNGAds/MNGAdsFull"
```

After running `pod install` (if you’re setting up Cocoapods for the first time) or `pod update` (if you’re adding MNGAds to an existing Cocoapods project), it will be ready to use the base MngAds SDK. » 

To use Ebeacon you have to add

```ruby
pod "MNGAds/MAdvertiseBeacon"
```

And add manually [BeaconForStoreSDK.framework] and [BeaconForStoreStorage.bundle] to your project.


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
pod "MNGAds/MNGAdsStandalone" //to add Only MNG ADSERVER + AppsFire
pod "MNGAds/AppsFire" //to add Only MNG ADSERVER + AppsFire
pod "MNGAds/Facebook" // to add Facebook Audience Network
pod "MNGAds/DFP" // to add DFP
pod "MNGAds/SmartAdServer" // to add SmartAdServer (SAS)
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
[libMAdvertiseB4SAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/MNGAds/libMAdvertiseB4SAdapter.a?at=master&fileviewer=file-view-default
[BeaconForStoreSDK.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/d41507a6c8eac3829efd9b05247acac1fcc51f8f/Demo/MNG-Ads-SDK/BeaconForStoreSDK.framework/?at=master
[BeaconForStoreStorage.bundle]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/BeaconForStoreStorage.bundle/?at=master