# upgrading SDK

## Upgrading to v2.0

### adNetworks
Removed:
- Appsfire (now is integrated on MNGAds)
- Mng Perf (now is integrated on MNGAds)
- Appnexus (now is integrated on MNGAds)

Added:
- LiveRail
- Flurry
- Amazon

### Integration

MNGAds v2.0 allow you to choose which adNetworks you will use, the integration process has changed.

##### Manual integration:

libMNGAds.a is always required and with it you have only Mng Perf and Appsfire works.

To add another adNetwork, you have to add to your project the lib[adNetworkAdapter].a and the adNetwork SDK.

*Example:* To use Smart Ad Server you have to add:
- libMNGAdsSASAdapter.a
- libSmartAdServer.a

**`Important :` If you add just lib[adNetworkAdapter].a, the dispatcher will not use it and if you just add the adNetwork SDK, you will have a compilation error:**
 ```
 References not found
 ```

##### CocoaPods integration

see [Using CocoaPods]

### MediaContainer

With MNGAds v2.0 you can integrate video ads into your Native Ad experience by calling [MNGNAtiveObject setMediaContainer:(UIView *)mediaContainer] and the SDK will add the video or the cover image to your container

```objc
-(void)adsAdapter:(MNGAdsAdapter *)adsAdapter nativeObjectDidLoad:(MNGNAtiveObject *)nativeObject{
    ...
    [nativeObject setMediaContainer:self.container];
    ...
}
```
coverImageUrl still available but it can be `nil`.

## Upgrading to v1.4.1 (Building Against iOS9)

iOS 9 introduces changes that are likely to impact your app and its MngAds integration.

- **[Learn what's new in iOS 9 from Apple]**
- **One of the changes in iOS9 is a default setting that requires apps to make network connections only over SSL ([App Transport Security]).** Therefore Whitelist Ads Servers for Network Requests, mngAds works under https but not all adNetworks on mediation (smartAdserver, appNexus, facebook, ...). if you want to release apps that build against iOS9, you will need to disable ATS in order to ensure all mediation works too.

```
#!objective-c
<key>NSAppTransportSecurity</key>
    <dict>
        <key>NSAllowsArbitraryLoads</key>
        <true/>
    </dict>

```

You can also edit the plist by adding NSAppTransportSecurity key of dictionary type with a dictionary element of NSAllowsArbitraryLoads of boolean type set to “Yes”.

![ats.png](https://bitbucket.org/repo/aen579/images/32376746-ats.png)

- **v1.4.1 of the SDK supports bitcode**. If you are using earlier versions, you must disable bitcode. **But for now GoogleMobileAds.framework do not support bitcode, therefore you must disable bitcode for your app**

>GoogleMobileAdsSdkiOS-7.4.1/GoogleMobileAds.framework/GoogleMobileAds(GADGestureIdUtil.o)' does not contain bitcode. You must rebuild it with bitcode enabled (Xcode setting ENABLE_BITCODE), obtain an updated library from the vendor, or disable bitcode for this target.

 - **FBAudienceNetwork.framework** and  **libSmartAdServer.a** do not work with **Xcode 6.4**. Therefore, MngAds needs **Xcode 7**.

## Upgrading to v1.4

Now appNexus is available on Cocoapods and pod generate libAppNexusSDK.a, you must remove libANSDK.a old librairy in order to avoid duplicate symbol.

## Upgrading to v1.3.2

The call to the following methods 

```
#!objective-c
-(BOOL)createInterstitialWithPreferences:(MNGPreference*)preferences autoDisplayed:(BOOL)autoDisplyed;  
-(BOOL)createInterstitialAutoDisplayed:(BOOL)autoDisplyed;
```

should be replaced by

```
#!objective-c
-(BOOL)createInterstitialWithPreferences:(MNGPreference*)preferences;
-(BOOL)createInterstitial;
```

## Upgrading to v1.2.1

Bug preference.keyword, now allow empty value if location is setted.

## Upgrading to v1.2

You must add **Appnexus** library. You must setpreference.keyword,if location is setted.(bug fix in v1.2.1)

## Upgrading from v1.0 to v1.1

The following methods have been changed. ```preferredHeight:(CGFloat)preferredHeight``` is now available to more easily resize banners.


```
#!objective-c

(void)adsAdapter:(MNGAdsAdapter *)adsAdapter bannerDidLoad:(UIView *)bannerView preferredHeight:(CGFloat)preferredHeight{
```


instead of


```
#!objective-c

(void)adsAdapter:(MNGAdsAdapter *)adsAdapter bannerDidLoad:(UIView *)bannerView{
```




 [Learn what's new in iOS 9 from Apple]:https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html
 [App Transport Security]:https://developer.apple.com/library/prerelease/ios/technotes/App-Transport-Security-Technote/



