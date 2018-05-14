# MAdvertiseVectaury

## Installation:
You will just need to specify the subspec for Vectaury since it s not included by default like so :

```
  pod "MNGAds",:subspecs => ["MNGAdsFull", "Vectaury"]
```

Also you need to make sure to add their Settings.bundle after the installation is complete https://cdn.vectaury.io/sdk/doc/ios/integration/)

### Initializing MAdvertiseVectaury
Once the installation has been successful you will need to initialise in application:didFinishLaunchingWithOptions:
```objc

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [MNGAdsSDKFactory initVectauryAfterInitialisedWithOptions:launchOptions];
}
```
 * notice: the actual initialisation of Vectaury will occur right after [MNGAdsSDKFactory initWithAppId:MNG_ADS_APP_ID] is executed, so in case you do not call on [MNGAdsSDKFactory initWithAppId:MNG_ADS_APP_ID] in the didFinishLaunchingWithOptions the initialisation of Vectaury will wait until initWithAppId is completed then initialise MAdvertiseData automatically, to summarise although initVectauryAfterInitialisedWithOptions has to be placed within didFinishLaunchingWithOptions, initWithAppId doesnt have to be placed there (optional), so wherever you place the initWithAppId everything would work as it s supposed to.