## Change log and release notes for the MngAds SDK for iOS.

See [Wiki] and [Help Center]  for more detailed informations.
you must check [Upgrade Guide]. You need to keep all Ad Network libs up to date.


## Version 3.3.2
#### Release date: June 15th, 2021
- **Requirements** 
    
    - Xcode 12.5

  - **Bug Fixes**

     - Fix issue local path "ld: library not found for -lBlueStack"
    
- **Ad Network Mediation Updates**
 
     - Use new [BlueStack-SDK] + *Adapter.a
     - Use new [BlueStack-SDK-Core] 
     - Use new [MAdvertiseLocation-v3.0.0]

## Version 3.3.1
#### Release date: June 14th, 2021
- **Requirements** 
    
    - Xcode 12.4


  - **Bug Fixes**

     - Fix crash [MNGInterstitialViewController present]
    
- **Ad Network Mediation Updates**
 
     - Use new [BlueStack-SDK] + *Adapter.a
     - Use new [BlueStack-SDK-Core] 
     - Use new [MAdvertiseLocation-v3.0.0]

## Version 3.3.0
#### Release date: June 7th, 2021
- **Requirements** 
    
    - Xcode 12.4


  - **Bug Fixes**

     - Fix viewability bug
     - Fix impscript bug
     - Fix IAS - OM SDK bug
     - Fix key/value madvertiseSSP bug
     - Fix OMSDK - VAST bug
     - Fix SKAdNetwork click

- **Features**

    - Manage smartAdserver Semantic 

- **Ad Network Mediation Updates**
 
     - Use new [BlueStack-SDK] + *Adapter.a
     - Use new [BlueStack-SDK-Core] 
     - Use new FacebookAudience 6.5.0 version [FBAudienceNetwork.framework] 
     - Use new DFP 8.5.0 version [GoogleMobileAds.xcframework]
     - Use new [MAdvertiseLocation-v2.3.1]
     - Use new AmazonPublisherServicesSDK 4.0.0 
     - Use new Smart-Display-SDK 7.10.1

## Version 3.2.4
#### Release date: March 25th, 2021
- **Requirements** 
    
    - Xcode 12.4

- **Features**
    - Replace iabtechlab.OMSDK by madvertisebluestack.OMSDK

## Version 3.2.3
#### Release date: March 12th, 2021
- **Requirements** 
    
    - Xcode 12.4
  
- **Features**

     - New Pod for [BlueStack-SDK-Core] without mediation dependencies
     - Measure ATT trackingAuthorizationStatus

```objective-c

 // ATTrackingManagerAuthorizationStatusNotDetermined = 0
        // ATTrackingManagerAuthorizationStatusRestricted =1
        // ATTrackingManagerAuthorizationStatusDenied=2
        // ATTrackingManagerAuthorizationStatusAuthorized= 3
```



- **Bug Fixes**

    - Fix duplicate intersitial  show issue 

- **Ad Network Mediation Updates**

    - Use new [BlueStack-SDK] + *Adapter.a
    - Use new AmazonPublisherServicesSDK 3.4.4

## Version 3.2.2
#### Release date: March 9th, 2021
- **Requirements** 
    
    - Xcode 12.4
​

- **Bug Fixes**

    - Fix inApp bidding keyValue Issue 
    - Fix intersitial issue showAdFromRootViewController 
 
## Version 3.2.1
#### Release date: February 26th, 2021
- **Requirements** 
    
    - Xcode 12.4
​

- **Bug Fixes**
​
    - Fix Bitcode activation 


## Version 3.2.0
#### Release date: February 16th, 2021
- **Requirements** 
    
    - Xcode 12.4

- **Features**
      - Prepare for iOS 14+ 
      - Upgrade OM SDK 1.3.16 
      - New AdFormat [Thumbnail Ads] For Ogury SDK.
      - Support of Facebook Audience Network bidding for in-app ads.
      - New Mngperf AdFormat RewardVideo
      - Enable SKAdNetwork to track conversions
      - mngPreference.setLanguage is now deprecated.

- **Bug Fixes**

    - Fix crash DTBAds.m line 74 
    - Fix ATTrackingManager issue
 
- **Ad Network Mediation Updates**

     - Use new [BlueStack-SDK] + *Adapter.a
   - Use new FacebookAudience 6.2.1 version [FBAudienceNetwork.framework] 
   - Use new DFP 8.0.0 version [GoogleMobileAds.xcframework]
   - Use new [MAdvertiseLocation-v2.3]
   - Use new appLovinSDK 6.15.1 
   - Use new adColony 4.5.0 version, [AdColony.framework]
   - Use new AmazonPublisherServicesSDK 3.4.2 
   - Use new CriteoPublisherSdk 4.2.1
   - Use new OguryAds 2.3.3


## Version 3.1.6
#### Release date: December 8th, 2020
- **Requirements** 
    - Xcode 12.2
 
- **Ad Network Mediation Updates**
   - Use new [BlueStack-SDK] + *Adapter.a
   - Use new FacebookAudience 6.2.0 version [FBAudienceNetwork.framework] 
   - Use new DFP 7.69.0 version [GoogleMobileAds.framework]


## Version 3.1.5
#### Release date: December 4th, 2020
- **Requirements** 
    - Xcode 12.2
 
- **Ad Network Mediation Updates**
    - Use new [BlueStack-SDK] + *Adapter.a
    - Use new OguryAds 2.3.2

## Version 3.1.4
#### Release date: November 11th, 2020
- **Requirements** 
    - Xcode 12.0.1
- **Bug Fixes**

    - fix crash [NSPlaceholderDictionary initWithObjects:forKeys:count:] .
   
- **Ad Network Mediation Updates**
    - Use new [BlueStack-SDK] + *Adapter.a
    - Use new Smart-Display-SDK 7.8.0


## Version 3.1.3
#### Release date: November 6th, 2020
- **Requirements** 
     - Xcode 12.0.1
- **Bug Fixes**

    - fix crash CoreTelephony .
    - fix crash [MNGAdsSDKFactory createInfeedInFrame withPreferences] .
    - fix crash [MNGAdsSDKFactory initRequest:preferences:error:] .
    - fix crash [MNGAdsSDKFactory sortAdsServersByPriority].
    - fix crash [MNGAdsAdapter setBannerDelegate:].
    - fix crash DFP nativeAd without cover adLoader:didReceiveUnifiedNativeAd.
    - fix bug infeed click .

- **Ad Network Mediation Updates**
    - Use new [BlueStack-SDK] + *Adapter.a
    - Use new [MAdvertiseLocation-v2.2]
    - Use new adColony 4.4.1.1 version, [AdColony.framework]
    - use the latest version OM SDK - 1.3.11


## Version 3.1.2
#### Release date: October 12th, 2020
- **Requirements** 
     - Xcode 12.0.1

- **Features**
      - Upgrade OM SDK 1.3.11 (viewability with VAST optimization)

- **Bug Fixes**

    - fix xcode 12 build simulateur .
    - fix crash [MNGAnalyticsManager sendAdRequestData]
 

- **Ad Network Mediation Updates**
    - Use new [BlueStack-SDK] + *Adapter.a
    - Use new DFP 7.66.0 version [GoogleMobileAds.framework]
    - Use new FacebookAudience 6.0.0 version [FBAudienceNetwork.framework]
    - use the latest version OM SDK - 1.3.11



## Version 3.1.1
#### Release date: October 6th, 2020
- **Requirements** 
    - Xcode 12.0.1
 
- **Ad Network Mediation Updates**
    - Use new [BlueStack-SDK] + *Adapter.a
    - Use new [MAdvertiseLocation-v2.1.1]


## Version 3.1.0
#### Release date: September 30th, 2020
- **Requirements** 
    - Xcode 12
    
- **Features**

 - Prepare for iOS 14 (https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/ios14) :

   
- **Ad Network Mediation Updates**
    - Use new [BlueStack-SDK] + *Adapter.a
    - Use new [MAdvertiseLocation-v2.1] (https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/change-log-madvertiselocation)


## Version 3.0.5
#### Release date: September 18, 2020
- **Requirements** 
    - Xcode 11.5
    
- **Features**

    -  Support for GDPR TCF v2 
   
- **Ad Network Mediation Updates**
    - Use new [BlueStack-SDK] + *Adapter.a
    - Use new [MAdvertiseLocation-v2.0].
    - Use new DFP 7.65.0 version [GoogleMobileAds.framework]
    - Use new adColony 4.1.5 version, [AdColony.framework]

## Version 3.0.4
#### Release date: July 23, 2020
- **Requirements** 
    - Xcode 11.5
    
- **Features**

    -  Support for GDPR TCF v1 
    -  implemented  new Function setLocationPreferences (**if you are use location data only**)
    
        * case consentFlag =  0  // user do not allow  
        * case consentFlag =  1 // user provide consent
        * case consentFlag =  2 // SDK must check consent IAB consent
        * case consentFlag =  3  //SDK must check Madvertise consent

```objc
    preferences.location = [preferences setLocationPreferences:[APP_DELEGATE sharedLocationManager].location WithConsentFlag: consentFlag] ;
```
      
 
- **Ad Network Mediation Updates**
    - Use new [BlueStack-SDK] + *Adapter.a
    - Use new [MAdvertiseLocation-v1.9].

## Version 3.0.3
#### Release date: Juin 26, 2020
- **Requirements** 
    - Xcode 11.5
    
- **Bug Fixes**
    - Fix inappBidding Crash Heap Corruption 
    - Fix URL Session Crash
 
- **Ad Network Mediation Updates**
    - Use new [BlueStack-SDK] + *Adapter.a
    - Use new CriteoPublisherSdk 3.7.0 
    - Use new Smart-Display-SDK 7.6.2


## Version 3.0.2
#### Release date: Juin 9, 2020
- **Requirements** 
    - Xcode 11.5
    
- **Bug Fixes**
    - Fix inappBidding crash Memory 
    - Fix Native Ad Crash
    - Fix save NSUserDefault crash
 
- **Ad Network Mediation Updates**
    - Use new [BlueStack-SDK] + *Adapter.a
    - Use new OguryAds 1.4.2 
    - use the latest version OM SDK - 1.3.5

## Version 3.0.1
#### Release date: May 26th, 2020 
- **Requirements** 
    - Xcode 11.3
    
- **Features**

    - New Native Ad Collection Callback click 
   
- **Ad Network Mediation Updates**
    - Use new [BlueStack-SDK] + *Adapter.a
    - Use new Smart-Display-SDK 7.6.0
    - Use new DFP 7.60.0 version [GoogleMobileAds.framework]
    - Use new adColony 4.1.5 version, [AdColony.framework]
    - Use new appLovinSDK 6.12.4 
    - Use new AmazonPublisherServicesSDK 3.3.1 
    - Use new CriteoPublisherSdk 3.5.0 
    - Use new OguryAds 1.4.1 


## Version 3.0.0
#### Release date: May 19th, 2020 
- **Requirements** 
    - Xcode 11.3
    
- **Features**
 - replace pod name  from MngAds to BlueStack-SDK 
 - In-App Bidding feature.
 - Support for Parallax on Infeed format
 - Add support for the Transparency and Consent Framework V2 (accept TCF v2 consentString https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20CMP%20API%20v2.md#what-is-the-cmp-in-app-internal-structure-for-the-defined-api).
 - Added OguryAds SDK (Version 1.3.2) 
 - Added Criteo SDK (Version 3.4.0) 
 
- **Bug Fixes**
    - Removed all references to **UIWebView**. **UIWebView** is no longer supported.
    - fix click Handler issue on Interstitial
 
- **Ad Network Mediation Updates**
    - Use new [BlueStack-SDK] + *Adapter.a
    - Use new Smart-Display-SDK 7.4.2
    - Use new DFP 7.58.0 version [GoogleMobileAds.framework]
    - Use new MoPub 5.12.1 version, [MoPub Marketplace] + [libMAdvertiseMoPubAdapter.a]
    - Use new adColony 4.1.4 version, [AdColony.framework]
    - Use new appLovinSDK 6.12.4 
    - Use new [MAdvertiseLocation-v1.8].
    - Use new FacebookAudience 5.9.0 version [FBAudienceNetwork.framework]
    - Use new Flurry 10.3.1 version [libFlurryAds] , [libFlurry]

## Version 2.16.3
#### Release date: February 26, 2020 
- **Requirements** 
    - Xcode 11.3
  
- **Bug Fixes**
    - Fix crash NSInternalInconsistencyException
    - Removed all references to **UIWebView**. **UIWebView** (Smart-Display-SDK) is no longer supported.
 
- **Ad Network Mediation Updates**
    - Use new [MngAdsSDK] + *Adapter.a
    - Use new Smart-Display-SDK 7.4.0
    - Use new DFP 7.55.1 version [GoogleMobileAds.framework]
    - Use new MoPub 5.11.0 version, [MoPub Marketplace] + [libMAdvertiseMoPubAdapter.a]

## Version 2.16.2
#### Release date: February 10, 2020 
- **Requirements** 
    - Xcode 11.3
  
- **Bug Fixes**
    - Fix Native Ad google  issue
    - Fix Google crash NSInternalInconsistencyException
    - Fix de debug mode MNGAdsMotionQueue
 
- **Ad Network Mediation Updates**
    - Use new [MngAdsSDK] + *Adapter.a
    - Use new FacebookAudience 5.6.1 version [FBAudienceNetwork.framework]
    - use new DFP 7.55.0 version [GoogleMobileAds.framework]


## Version 2.16.1
#### Release date: January 27, 2020
- **Requirements** 
    - Xcode 11.3

- **Features**
    - New Native Ad Collection implementation with Cover Image
   
- **Bug Fixes**
    - Fix Dissmis Bug ios 13 : appsfire interstial 
    - Fix NSCalendarsUsageDescription issue
    - FIx Session OMSDK issue 

## Version 2.16
#### Release date: January 8, 2020
- **Requirements** 
    - Xcode 11.3

- **Features**
    - use the latest version OM SDK - 1.2.19.
    - New Native Ad implementation with Cover Image
   
- **Bug Fixes**
    - Fix status Bar bug 
    - Fix bug capping
    - Fix appsfire interstial bug 
    - Fix mute issue

- **Ad Network Mediation Updates**

    - Use new [MngAdsSDK] + *Adapter.a
    - use new DFP 7.53.1 version [GoogleMobileAds.framework]
    - Use new FacebookAudience 5.6.0 version [FBAudienceNetwork.framework]
    - Use new [MAdvertiseLocation-v1.7].


## Version 2.15.1
#### Release date: October 1, 2019
- **Requirements** 
    - Xcode 11.2
- **Features**
    - Remove the UIWebview
    - use the latest version OM SDK - 1.2.19.
    - New BlueStack Demo application
   
- **Bug Fixes**
    - fix the crash nslogv

- **Ad Network Mediation Updates**

    - Use new [MngAdsSDK] + *Adapter.a
    - use new DFP 7.50.0 version [GoogleMobileAds.framework]
    - Use new FacebookAudience 5.5.1 version [FBAudienceNetwork.framework]
    - Use new AdColony 4.1 version, [AdColony.framework]

## Version 2.15
#### Release date: September 18th, 2019
- **Requirements** 
    - Xcode 11.3.2
- **Features**
    - iOS13 support
    - Added AppLovin SDK for mediation.
    - mngAdsSDKFactoryDidResetConfig is now deprecated to avoid confusion
    - Dispatcher cache optimization
    - New infeed size constant(INFEED_RATIO_16_9 / INFEED_RATIO_4_3)


- **Bug Fixes**
    - Fix mute issue
    - Fix Debug gyro issue

- **Ad Network Mediation Updates**

    - Use new [MngAdsSDK] + *Adapter.a
    - Use new Smart-Display-SDK 7.2.0
    - Use new FacebookAudience 5.5.0 version [FBAudienceNetwork.framework]
    - use new DFP 7.49.0 version [GoogleMobileAds.framework]
    - Use new Flurry 9.3.1 version [libFlurryAds] , [libFlurry]
    - Use new MoPub 5.9.0 version, [MoPub Marketplace] + [libMAdvertiseMoPubAdapter.a]
    - Use new AdColony 3.3.8.1 version, [AdColony.framework]
    - Use new [MAdvertiseLocation-v1.6].

## Version 2.14.2
#### Release date: August 16th, 2019

- **Bug Fixes**

    - fix crash MNGAdsMotionQueue 

- **Ad Network Mediation Updates**

    - Use new [MngAdsSDK] + *Adapter.a
    - use new DFP 7.48.0 version [GoogleMobileAds.framework]:
    - Use new [MAdvertiseLocation-v1.4].

## Version 2.14.1
#### Release date: July 25th, 2019

- **Bug Fixes**

    - restore DFP 7.42.1 version [GoogleMobileAds.framework], on 2.14 there was 7.31.0

## Version 2.14
#### Release date: July 24th, 2019

- **Features**
    - New AmazonAPS mediation adapter.
    - Fresh initialization after an update of the sdk.
    - Viewability feature to track how much of the ad had been seen.
    - VAST4 and VAST4 wrapper support for Madvertise Adserving
    - Enabling debug MAdvertiseLocation sdk along with the MAdvertise SDK.
    - compliant to xcode 10.2 and swift 5
    - New nativeAd for Facebook Audience Network and Mopub, **You must check [Upgrade Guide], implementation has changed**
    - Blocked the following ad networks when they are disabled by cmp: Facebook Audience, Amazon Publisher Service (require [MadvertiseCMP v21](https://bitbucket.org/mngcorp/madvertise-gdpr-cmp-ios/downloads/) ).
    - Blocked retency when it is disabled by cmp (require [MadvertiseCMP v21](https://bitbucket.org/mngcorp/madvertise-gdpr-cmp-ios/downloads/) ).

- **Bug Fixes**

    - fix crash mopub crashes
    - fix minor bugs.

- **Ad Network Mediation Updates**

    - Use new [MngAdsSDK] + *Adapter.a
    - Use new FacebookAudience 5.4.0 version [FBAudienceNetwork.framework]
    - Use new [AmazonPublisherService](https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/AmazonPublisherService)

## Version 2.13.3
#### Release date: April 29th, 2019

- **Features**
 
   - Add DFP Infeed
   - Change the native ad DFP 
   - Remove Vectaury

- **Bug Fixes**

    - fix crash SendSynchronousRequest / loadRequest
    - fix minor bugs.


- **Ad Network Mediation Updates**

    - Use new [MngAdsSDK] + *Adapter.a
    - use new DFP 7.42.1 version [GoogleMobileAds.framework]:

**`Important :`You should note that it is mandatory that you add to your .plist file:**
```
<key>GADIsAdManagerApp</key> 
<true/>
```
**Also you need to add the -ObjC linker flag to Other Linker Flags in your project's build settings **, for more on this checkout : 
https://developers.google.com/ad-manager/mobile-ads-sdk/ios/quick-start#update_your_infoplist

## Version 2.13.2
#### Release date: April 8th, 2019

- **Ad Network Mediation Updates**

    - Use new [MAdvertiseLocation-v1.3].

## Version 2.13.1
#### Release date: March 19th, 2019

- **Features**
 
   - Improve the custom close button iteractions on Interstitials.
   - Fix bug where click doesn't occur on certain Ads.
   - Change the display style of Interstitials to be always on top and FullScreen.

- **Ad Network Mediation Updates**

    - Use new [MngAdsSDK] + *Adapter.a
    - Use new [MAdvertiseLocation-v1.2].


## Version 2.13
#### Release date: February 25th, 2019

- **Features**
 
     - emphasize on executing init everytime the app runs.
     - support smart v7.
     - better support vast.
     - add OMSDK to debug gyro.
     - support arm64e (new iphones).
     - Remove B4S.

- **Ad Network Mediation Updates**

    - Use new [MngAdsSDK] + *Adapter.a
    - Use new smart v7.
    - Use new [MAdvertiseLocation-v1.1].
    - Remove support for Beacon4Store B4S.

## Version 2.12.3
#### Release date: January 11th, 2018

- **Features**
 
   - You can now display interstitials using a new method [(more infos)]

- **Ad Network Mediation Updates**

    - Use new [MngAdsSDK] + *Adapter.a

## Version 2.12.2
#### Release date: January 7th, 2018

- **Bug Fixes**
 
   - Fix click issue on some implementation for smartAdserver (use View Controller of Factory)

- **Ad Network Mediation Updates**

    - Use new [MngAdsSDK] + *Adapter.a

## Version 2.12.1
#### Release date: Dec 13th, 2018
- **Features**

    - Remove MAdvertiseConsent class: this class became obsolete since MNGAds will be recovering the consent string directly from the UserDefaults using the official keys set by IAB.
    - New [MAdvertiseLocation] Adapter

- **Bug Fixes**

    - fix consent string update bug.

- **Ad Network Mediation Updates**

    - Add new [MAdvertiseLocation-v1.0]
    - Use new [MngAdsSDK] + *Adapter.a

## Version 2.12
#### Release date: Nov 13th, 2018

- **Bug Fixes**

    - fix bitcode support.
    - fix mopub crash when trying to load banners.

- **Ad Network Mediation Updates**

    - Use new Flurry 9.2.1 version [libFlurryAds] , [libFlurry]
    - Use new [MngAdsSDK] + *Adapter.a
    - Use new MoPub 5.4.0 version, [MoPub Marketplace] + [libMAdvertiseMoPubAdapter.a]

## Version 2.11.1
#### Release date: October 17th, 2018

- **Features**

 - For cocoapod users, OMSDK_Madvertise-x.framework is include into our pod as subspec
 - For manual install OMSDK_Madvertise-x.framework into https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/MNGAds-v2.11.1.zip

## Version 2.11
#### Release date: October 12th, 2018

- **Features**
     - ![omsdk.png](https://bitbucket.org/repo/GyRXRR/images/3400517277-omsdk.png) IAB Open Measurement compliant (viewability https://iabtechlab.com/technology-compliant-companies/#)
     - GDPR : Automatic consent management (from CMP) so you don't have to export it manually to the sdk, MAdvertiseConsent is now deprecated.
     - preferredHeight for infeed.
     - Support iOS 12.


- **Bug Fixes**

    - fix adrequest-adn bug where it was only sent in debug mode.
    - fix issue where the ad was requested twice.
    - fix minor bugs.
    - Updated sound management on video ads.

- **Ad Network Mediation Updates**

    - Use new AdColony 3.3.4 version, [AdColony.framework]
    - Use new Vectaury 1.6.3 version, [Vectaury.framework]
    - Use new GoogleMobileAds 7.31.0 version [GoogleMobileAds.framework]
    - Use new FacebookAudience 4.28.1 version [FBAudienceNetwork.framework]
    - Use new Flurry 9.0 version [libFlurryAds] , [libFlurry]
    - Use new SmartAdServer 6.10 version [libSmartAdServer.a]
    - Use new AmazonAd SDK 2.2.17.0 version [AmazonAd.framework]
    - Use new MoPub 5.3.0 version, [MoPub Marketplace] + [libMAdvertiseMoPubAdapter.a]
    - Use new [MngAdsSDK] + *Adapter.a
    - Add [OMSDK_Madvertise-x.framework]

All *Adapter.a available on https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/MNGAds-v2.11.zip

and [OMSDK_Madvertise-x.framework]

## Version 2.10
#### Release date: May 11th, 2018

- **Features**

     - Support window.open to track clicks.
     - Mediation: added support for AdColony.
     - Mediation: added support for Vectaury ([MAdvertiseVectaury]).
     - Eyes detection feature now support landscape mode.
     - According to the General Data Protection Regulation, we now have the option to provide the consent strings to MAdvertise. See [GDPR] doc.


- **Bug Fixes**

    - fix scrollable interstitials.
    - fix minor bugs.

- **Ad Network Mediation Updates**

    - **Add new AdColony 3.3.0 version, [AdColony.framework]**
    - **Add new Vectaury 1.5.2 version, [Vectaury.framework]**
    - Use new GoogleMobileAds 7.30.0 version [GoogleMobileAds.framework]
    - Use new FacebookAudience 4.28.1 version [FBAudienceNetwork.framework]
    - Use new Flurry 8.5.0 version [libFlurryAds] , [libFlurry]
    - Use new SmartAdServer 6.9 version [libSmartAdServer.a]
    - Use new [MngAdsSDK] + *Adapter.a

All *Adapter.a available on https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/MNGAds-v2.10.zip

## Version 2.9.1
#### Release date: March 15th, 2018

- **Features**

     - Support transparent interstitials (smartAdserver + MAS).
     - Implement a new way to track clicks on ads.
     - Improve pixel impression tracking.
     - Edit c_facedetection = 0 if the user refuses to grant permission to use the camera (Eyes Tracking).
     - Support native ad video and vast (MAS).

- **Bug Fixes**

    - fix (null) inall bug.
    - Fix custom close button on mraid interstitials.
    - Fix high cpu usage bug when app goes to background.

- **Ad Network Mediation Updates**

    - **Add new MoPub 4.20.1 version, [MoPub Marketplace] + [libMAdvertiseMoPubAdapter.a]**
    - Use new GoogleMobileAds 7.29.0 version [GoogleMobileAds.framework]
    - Use new FacebookAudience 4.28.0 version [FBAudienceNetwork.framework]
    - Use new BeaconForStoreSDK 2.2.14 version
    - Use new Flurry 8.4.0 version [libFlurryAds] , [libFlurry]
    - Use new [MngAdsSDK] + *Adapter.a

## Version 2.9
#### Release date: February 6th, 2018

- **Features**

     - The SDK can now handle multiple App_IDs in the same app without causing any issues.
     - Eyes tracking feature extended to include native ads as well.
     - New delegate method to notify the publisher if the sdk fails its initialization.
     - Improve dispatcher Ad Network tracking for MAT (adrequest-adn).
     - New attribute in MNGPreference to set [Native Ad Choice position]s.
     - Support native video ads provided by smartAdserver.

- **Bug Fixes**

    - Fix nil value for [MNGAdsSDKFactory isInitialized] right after running the app, now it will always contain the correct value.
    - Fix null version and app_id for the adrequest api.
    - Fix amazon banner ad size (**important**).

- **Ad Network Mediation Updates**

    - **Add new MoPub 4.15.0 version, [MoPub Marketplace] + [libMAdvertiseMoPubAdapter.a]**
    - Use new GoogleMobileAds 7.27.0 version [GoogleMobileAds.framework]
    - Use new FacebookAudience 4.27.2 version [FBAudienceNetwork.framework]
    - Use new BeaconForStoreSDK 2.2.13 version
    - Use new [MngAdsSDK] + *Adapter.a

## Version 2.8.1
#### Release date: December 21th, 2017

- **Features**

     - Use Browser user-agent for headers of all requests.
     - Support iPhone X and IOS11 for banner (UIScrollViewContentInsetAdjustmentNever, useful in full screen applications.)

- **Bug Fixes**

    - Fix mraid rendering and click on MAS ads.
    - Fix the the category issue of the AVAudioSession
    - Fix DFP's adchoice misposition issue on [nativead format].
    - Fix RewardedVideoAd delegate methods where in some scenarios didFail was not called.

- **Ad Network Mediation Updates**

    - Use new Flurry 8.3.4 version [libFlurryAds] , [libFlurry]
    - Use new AmazonAd SDK 2.2.15.1 version [AmazonAd.framework]
    - Use new [MngAdsSDK] + *Adapter.a



## Version 2.8
#### Release date: November 23th, 2017
- **Features**
    - Support iPhone X.
    - Full support for ios11 and xcode 9.
    - Implemented new preferredHeight logic for banner ads and MAS.
    - New [Rewarded Video for iOS].
    - New reset SDK button in debug gyro.
    - now MAS support video and vast format for infeed, interstitial and medium rectangle
    - New blurry background for video ads (multiple formats).
    - Eyes tracking Optimizations



- **Bug Fixes**
    - manage WKWebView or UIWebView server side to avoid clicks issues


- **Ad Network Mediation Updates**
    - use new GoogleMobileAds 7.26.0 version [GoogleMobileAds.framework]
    - use new Flurry 8.3.1 version [libFlurryAds] , [libFlurry]
    - use new SmartAdServer 6.7.2 version [libSmartAdServer.a]
    - use new [MngAdsSDK]

## Version 2.7.2
#### Release date: September 18th, 2017

- Fix crash with WKWebView's handler delegate.
- use new [MngAdsSDK]


## Version 2.7.1
#### Release date: September 18th, 2017

- New feature: Implementing the new eyes detection feature in Mraid ads.
- Edit Vast ads selecting mediaUrl algorithm to prioritize videos(mp4/3gpp) over vpaid ads.
- use new GoogleMobileAds 7.23.0 version [GoogleMobileAds.framework]
- use new Flurry 8.2.1 version [libFlurryAds] , [libFlurry]
- use new BeaconForStoreSDK 2.2.12 version [BeaconForStoreSDK.framework]



## Version 2.7
#### Release date: August 28th, 2017

- Migrate from using UIWebView to MKWebView , although UIWebView still available for iOS7 users.
- BeaconForStoreSDK isnt available by default when installing from cocoapods, to install it you will need to specify its subspec :

```
pod "MNGAds",:subspecs => ["MNGAdsFull", "B4S"]
```
- New menu in the demo showing how to use our MoPub adapter.
- New menu in the demo to try out only appsfire ads.
- AdChoice view available in all formats.
- Implementing new methodology to track impressions using impression script along side impression url.
- Fix minor bugs , including the muted sound issue.

- use new FacebookAudience 4.25.0 version 
- use new GoogleMobileAds 7.22.0 version 
- use new SmartAdServer 6.7.1 version 
- use new BeaconForStoreSDK 2.2.9 version 

## Version 2.6
#### Release date: June 23th, 2017

- Implemented new **eyes tracking** feature in MAdvertiseAdserver (MAS) that tracks the user's face to determine if he is really watching the ad or not , and for how long. You need to include [umoove.framework] in your project
- New infeed ad format in mngadserver (MAS).
- New features in debug gyro.
- Disable scroll in some banners.
- Fix possible bug where the cascade would be blocked without returning a valid ad nor a fail error.
- Edit impression requirements.
- Fix banner size bug.
- Fix clickUrl issue.
- Remove spaces from keywords.


- use new FacebookAudience 4.23.0 version [FBAudienceNetwork.framework]
- use new GoogleMobileAds 7.20.0 version [GoogleMobileAds.framework]
- use new Flurry 8.1.0 version [libFlurryAds] , [libFlurry]
- use new BeaconForStoreSDK 2.2.8 version [BeaconForStoreSDK.framework]


## Version 2.5.3
#### Release date: April 24th, 2017

- fix supported architectures issue where you get differents warnings about different adapters not supporting some architectures,in some cases it goes as far as saying that some adapters cannot be found during runtime.

- use new Flurry 8.0.1 version [libFlurryAds] , [libFlurry]


## Version 2.5.1
#### Release date: April 19th, 2017

- use new FBAudienceNetwork v4.22.0 version [FBAudienceNetwork.framework] (Fixed a critical bug that the image ad content is not rendered in FBMediaView.)


## Version 2.5
#### Release date: April 17th, 2017

 - Some methods in MNGAdsFactory are now deprecated and will be removed in next version:

| Depecated method | New method |
| --- | --- |
| createBanner() | loadBanner() |
| createBanner(MNGFrame frame) | loadBanner(MNGFrame frame)  |
|createBanner(MNGPreference preference)|loadBanner(MNGPreference preference)   |
|createBanner(MNGFrame frame, MNGPreference preference)|loadBanner(MNGFrame frame, MNGPreference preference) |
|createInterstitial()|loadInterstitial()   |
|createInterstitial(boolean autoDisplay)|loadInterstitial(boolean autoDisplay)  |
|createInterstitial(MNGPreference preference)|loadInterstitial(MNGPreference preference)   |
|createInterstitial(MNGPreference preference, boolean autoDisplay)|loadInterstitial(MNGPreference preference, boolean autoDisplay)   |
|createNative()|loadNative()   |
|createNative(MNGPreference preference)|loadNative(MNGPreference preference)   |
|createNativeCollection(int requestedAdNumber)|loadNativeCollection(int requestedAdNumber)  |
|createNativeCollection(int requestedAdNumber, MNGPreference preference)|loadNativeCollection(int requestedAdNumber, MNGPreference preference)   |
|createInfeed()|loadInfeed() |
|createInfeed(MNGFrame frame)|loadInfeed(MNGFrame frame) |
|createInfeed(MNGPreference preference)|loadInfeed(MNGPreference preference) |
|createInfeed(MNGFrame frame, MNGPreference preference)|loadInfeed(MNGFrame frame, MNGPreference preference) |

- MAdvertiseError : in case of fail, the didFail delegate method will be invoked with an MAdvertiseError, you want to check which error was invoked by checking its code and description and matching it with the predefined MAdvertiseErrors (see Error Handling in the documentation for more info).
- persisent seenAd : seenAd is now managed in the sdk cache without life time.
- native ad adChoice : adserver can return an adchoice view for native ad.
- clarify doc about native ad registerViewForInterraction.
- add crashlitycs in MngAdsDemo. 
 - Fixed bugs:
   - Null values in Request : don't send the parameter to the adNetwork if it is null or empty.
   - Inall : fix dfp custom targetting and key words.

Don't forget to update following libraries :

- [MngAdsSDK]
- [FBAudienceNetwork.framework]
- [GoogleMobileAds.framework]
- [BeaconForStoreSDK.framework]

## Version 2.4.1
#### Release date: March 22th, 2017

 - fix crash for appsfire banner

Don't forget to update following libraries :

- [MngAdsSDK]

## Version 2.4
#### Release date: March 10th, 2017

- use new SmartAdServer 6.6.1 version [libSmartAdServer.a]
- use new Flurry 7.10.0 version [libFlurryAds] , [libFlurry]
- use new B4S 2.1.10 version [BeaconForStoreSDK.framework]
- use new Google-Mobile-Ads-SDK 7.18.0 version [GoogleMobileAds.framework]
- use new FBAudienceNetwork 4.20.0 version [FBAudienceNetwork.framework]
- improve AppsFire cache managment
- add support for vast inline
- new Interstitiel management pattern: once you have an interstitiel loaded all new requests to create a new one (w/ same placement and viewController) will hand out the already loaded interstitiel instead of creating a new request.
- new inall targetting
- badge in the nativeAd is customizable now using the method:

```
    [_nativeObject updateBadgeTitle:@"newBadgeTitle"];

```

>note that the new method returns a BOOL indicating if the update was successful or not.

- contentUrl: new attribut in MNGPreference : now you can pass to the sdk an URL for content related to your app (url must be a string which length do not exceed 512 characters)
- persistent capping : capping is now managed on cache.
- memory management improvement.
- fix minor bugs.

## Version 2.3.4
#### Release date: January 27th, 2017

- use new B4S 6.6 version [BeaconForStoreSDK.framework]
- use new Flurry 7.9.2 version [libFlurry] [libFlurryAds]
- improve AppsFire cache managment
- add *Shake To Debug* system, [debug-mode-gyro]
- add support contentURL for DFP
- improve Demo:
    - add pager sample: contains infeed page and a native ad page, https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/PagerViewController.m?at=master&fileviewer=file-view-default
    - improve InfeedViewController: add a native parallax imageView and custom parallax navigationBar
    - improve SwiftViewController: now the sample contains all formats, https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/SwiftViewController.swift?at=master&fileviewer=file-view-default


## Version 2.3.3
#### Release date: December 21th, 2016

 - use new SmartAdServer 6.6 version [libSmartAdServer.a]

## Version 2.3.2
#### Release date: December 19th, 2016

**This version is ATS-compliant, If you push you submit an app after 1th January 2017, you must use this version.**

[App Transport Security] improves privacy and data integrity by ensuring your app’s network connections employ only industry-standard protocols and ciphers without known weaknesses. This helps instill user trust that your app does not accidentally leak transmitted data to malicious parties.

MNGAds SDK (with Mediation) are now ATS-compliant, but a small percentage of creatives (near to zero) not directly hosted on our platform are not.

If you must make an exception for a reason, we recommend that you minimize it by only setting the NSAllowsArbitraryLoadsInWebContent and NSAllowsArbitraryLoadsForMedia keys,
```xml
<key>NSAppTransportSecurity</key>
    <dict>
        <key>NSAllowsArbitraryLoadsForMedia</key>
            <true/>
        <key>NSAllowsArbitraryLoadsInWebContent</key>
            <true/>
    </dict>
```

- new template interstitial and square (Appsfire)
- add pod dependency for B4S (If you are using cocoapods, you must remove BeaconForStoreSDK.framework/BeaconForStoreSDK, it will be auto-downloaded by cocoapods)
- use new AdNetworks version:
- use new FBAudienceNetwork 4.18.0 version [FBAudienceNetwork.framework]
- use new DFP 7.16.0 version [GoogleMobileAds.framework]
- use new Flurry 7.8.2 version [libFlurry_7.8.2.a] [libFlurryAds_7.8.2.a]
- use new BeaconForStore 2.0.14 version [BeaconForStoreSDK.framework]

Don't forget to update following libraries :


- [MngAdsSDK]
- [FBAudienceNetwork.framework]
- [GoogleMobileAds.framework]
- [libFlurry_7.8.2.a] [libFlurryAds_7.8.2.a]
- [BeaconForStoreSDK.framework]


## Version 2.3.1
#### Release date: November 11th, 2016

 - core optimization (dispatcher)
 - use new SmartAdServer 6.5 version [libSmartAdServer.a]
 - Remove NSCalendarsUsageDescription permission

Don't forget to update following libraries :


- [MngAdsSDK]
- [libSmartAdServer.a]

## Version 2.3
#### Release date: October 28th, 2016

 - Now MNGADS becomes MADVERTISE MEDIATION and MADVERTISE ADSERVING
 - VAST 2 /VPAID 1 support for MADVERTISE ADSERVING
 - Upgrading MADVERTISE MEDIATION libraries
 - Improve Native Ad assets management with 
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
 - Cache Optimisations
 - Bugs fixes
 - Memory leak fix for banner

Now you can add beacon for store:

- Get Ebeacon technology to propose to the advertisers to target the users inside the point of sale. 
- An installation base of 12,500 ebeacons ready to track the users.
- An exclusive format in Push notification to the users inside a tabacco shop, press shop, pharmay or mall.

### Initializing Beacons
You have to add libMAdvertiseB4SAdapter.a, BeaconForStoreSDK.framework and BeaconForStoreStorage.bundle to your project.



To access to beacon you have to use the MAdvertiseBeacon singleton. To initialise it you have to call the method initBeacon at application:didFinishLaunchingWithOptions:

```objc
#import <MAdvertiseBeacon.h>
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [MNGAdsSDKFactory initWithAppId:MNG_ADS_APP_ID];
    [[MAdvertiseBeacon singleton]initBeacon];
    //
}
```

### handleNotificationWithUserInfo
To handle beacon local notification, firstable you have to cheack if it is a beacon notification and let MAdvertiseBeacon handle it.

```objc
-(void)application:(UIApplication *)application didReceiveLocalNotification:(UILocalNotification *)notification{
    if ([[MAdvertiseBeacon singleton]userInfoIsBeaconNotification:notification.userInfo]) {
        [[MAdvertiseBeacon singleton]handleNotificationWithUserInfo:notification.userInfo];
    }else{
        //
    }
}
```


Don't forget to update following libraries :

- [MngAdsSDK]
- [FBAudienceNetwork.framework]
- [libFlurry], [libFlurryAds]
- [libSmartAdServer.a]
- [GoogleMobileAds.framework]

## Version 2.2.1
#### Release date: September 9th, 2016
 -  iOS 10 support, with Limit Ad Tracking changes (in this case we are using vendorId)
 - Now appsfire support videos for square, nativeAds and interstitials
 - Don't forget to update following libraries or use **pod update** :

    - [MngAdsSDK]
    - [FBAudienceNetwork.framework]
    - [AmazonAd.framework] (>= IOS8)
    - [libSmartAdServer.a]

## Version 2.2
#### Release date: August 29th, 2016

 - HTTPS support
 - New appsfire template for banner, medium rectangle and interstitial
 - New Google DFP librairie

Don't forget to update following libraries or use **pod update** :

 - [MngAdsSDK]
 - [GoogleMobileAds.framework]

## Version 2.1.2
#### Release date: July 22th, 2016

no changes, just fix wrong [libSmartAdServer.a] lib on cocoapods.org if pod update has been done on 2016-07-13.

## Version 2.1.1
#### Release date: July 13th, 2016


 - Use lastest smart Adserver and Facebook version
 - Now Amazon available with cocoapods (**If you are using cocoapods, you must remove AmazonAd.framework, it will be auto-downloaded by cocoapods**)
 - Now you can use new predifined sizes 
```objc
extern MNGAdSize const kMNGAdSizeDynamicBanner; //Small Banner Screen width x 50
extern MNGAdSize const kMNGAdSizeDynamicLeaderboard; //Landscape Banner ipad Screen width x 90
```

Don't forget to update following libraries :

 - [MngAdsSDK]
 - [FBAudienceNetwork.framework]
 - [libFlurry], [libFlurryAds]
 - [libSmartAdServer.a]

## Version 2.1
#### Release date: June 21th, 2016

 - Native Ad, add the "AdChoice" badge view for Google/Adx certification in addition to Ad" badge view.
 - Add Smart [In-Feed Ad format] (Parallax or Video)
 - Fixes for smart crashes (ARC
 - Improve mng adserving (interstitial capping, keywords)
 - Improve logging system
 - Add listener for refresh event
 - Remove [LiveRailSDK.framework]
 - Don't forget to update following libraries :
    - [MngAdsSDK]
    - [FBAudienceNetwork.framework]
    - [AmazonAd.framework]
    - [libFlurry], [libFlurryAds]
    - [libSmartAdServer.a](SDK has been converted to ARC for better memory management)

## Version 2.0.8
#### Release date: April 6th, 2016

**You must update [MngAdsSDK] lib and [mnAds Adapters]**

 - bug fixes IOS7 [MngAdsSDK] (after interstitial clicks)
 - upgrade [MngAdsSDK], now appsfire banner allow UIViewAutoresizingFlexibleWidth;


## Version 2.0.7
#### Release date: March 29th, 2016

**You must update [MngAdsSDK] lib and [mnAds Adapters]**

 - bug fixes IOS7 [FBAudienceNetwork.framework], [MngAdsSDK]
 - upgrade [MngAdsSDK], now appsfire banner allow UIViewAutoresizingFlexibleWidth;
 - now mngAds ignores createInterstial 5 secondes after disappear event to avoid overlaping
 - change default_subspec for cocoapods in order to avoid pod update without adapaters (new architecture of v2)

## Version 2.0.6
#### Release date: March 17th, 2016

**You must update [MngAdsSDK] lib and [mnAds Adapters]**

 - upgrade [LiveRailSDK.framework], 
 - bug fixes IOS7 [FBAudienceNetwork.framework], [MngAdsSDK]

## Version 2.0.5
#### Release date: March 13th, 2016

**You must update [MngAdsSDK] lib and [mnAds Adapters]**

 - Optimisation appsfire
 - bug fixes (liverail)

## Version 2.0.4
#### Release date: March 7th, 2016
 - Separate between request and display (see [Interstital implementation])
 - bug fixes

## Version 2.0.3
#### Release date: February 17th, 2016
You need to keep all Ad Network libraries up to date.

 -  Automatic Status bar management (to avoid https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/faq#markdown-header-how-do-i-hide-the-status-bar-on-interstitials-for-sdk-version-203)
 - fix issue for flurry interstitials
 - bug fixes


## Version 2.0.1
#### Release date: February 3th, 2016
You need to keep all Ad Network libraries up to date.

 - Fix compilation errors on simulator

## Version 2.0
#### Release date: January 28th, 2016


 - [libAppsfireSDK.a], [libANSDK] and [libMng-perf.a] libraries have been merged on [MngAdsSDK] SDK for better performance and reduce libraries number
 - We have added [AmazonAd.framework], [LiveRailSDK.framework] , [libFlurryAds_7.3.0.a] to mngads mediation in order to increase fill rate and revenus


## Version 1.5

#### Release date: November 19th, 2015

 - New appsfire SDK that use mngads adserver
 - New DFP version
 - Banner improvement for dynamic height

**You must update [MngAdsSDK], [libAppsfireSDK.a] and [GoogleMobileAds.framework]**


## Version 1.4.3

#### Release date: October 23th, 2015

 - bug fix (EXC_BAD_ACCESS and Facebook)

**You must update [MngAdsSDK]**

## Version 1.4.2

#### Release date: October 16th, 2015

 - use audienceNetwork pod (Facebook)
 - Fixed issue for Appsfire SDK
 - Interstitial improvement, now `isInterstitialShowen` is managed by SDK

**You must update [MngAdsSDK], [libAppsfireSDK.a] and [FBAudienceNetwork.framework]**

## Version 1.4.1

#### Release date: September 18th, 2015


 - IOS9 support (need to disable ATS and disable bitcode (google SDK do not support it) )

>GoogleMobileAdsSdkiOS-7.4.1/GoogleMobileAds.framework/GoogleMobileAds(GADGestureIdUtil.o)' does not contain bitcode. You must rebuild it with bitcode enabled (Xcode setting ENABLE_BITCODE), obtain an updated library from the vendor, or disable bitcode for this target.

**You must update [MngAdsSDK], [libMng-perf.a] , [libSmartAdServer.a] (not available from pod update), [FBAudienceNetwork.framework], [GoogleMobileAds.framework], [libAppsfireSDK.a] and [libANSDK]**

 - **FBAudienceNetwork.framework** and  **libSmartAdServer.a** do not work with **Xcode 6.4**. Therefore, MngAds needs **Xcode 7**.

## Version 1.4

#### Release date: August 25th, 2015


- appNexus can be used download via our Cocoapods
- New SmartAdServer-iOS-SDK-6.0 (dynamicAd, prefetch)
- Add ClickDelegate, The clickDelegate notify you when the ad has been clicked.
- Manage banner size (fixed or responsive) server side
- nativeAd, now we support DFP for premium nativeAd
- Bugs fixing (retain issue, ...)

You must update [MngAdsSDK], [libSmartAdServer.a] (not available from pod update), [FBAudienceNetwork.framework], [GoogleMobileAds.framework] and [libANSDK]

## Version 1.3.9

#### Release date: August 7th, 2015

 - Update Facebook Audience Network library

 - Update [MngAdsSDK] library.

## Version 1.3.8

#### Release date: July 28th, 2015

 - Fix memory issue with smart adapter

 - Update [MngAdsSDK] library.

## Version 1.3.7

#### Release date: July 21th, 2015

  - Update mng perf to 5.1.1 (fix html interstitial issue)

- Update [MngAdsSDK] and [libMng-perf.a] libraries

## Version 1.3.6

#### Release date: July 8th, 2015

  - Manage keywords from mngads console
  - mngperf Adserving improvement (geoloc)

- Update [MngAdsSDK] and [libMng-perf.a] libraries

## Version 1.3.4

#### Release date: June 11th, 2015

 - AdRequest improvement

## Version 1.3.3

#### Release date: June 3th, 2015

 - Manage dynamic size for DFP and appNexus banners
 - Add remote debug mode
 - Add ```@property MNGPriceType priceType;``` and ```@property NSString *localizedPrice;``` on MNGNAtiveObject (use for display "free" icon)
 - Add [Best practice Mngads], optimized use case for several ad formats on one page
 - Update [MngAdsSDK],[libAppsfireSDK.a], [libMng-perf.a] and [GoogleMobileAds.framework] libraries

## Version 1.2.3

#### Release date: May 1st, 2015

 - capping improvement
 - solved smart banner impressions
 - Add guidelines, https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/guidelines

## Version 1.2.2

#### Release date: April 21th, 2015

 - update appsfire SDK to 2.7.1 that use banner in 50pt
 - Improvement of appsfire nativeAd
 - Keywords are now available for all adNeworks with key/value system
 - Added bridge file for swift compatibility

## Version 1.2.1

#### Release date: April 10th, 2015

 - Bug preference.keyword, now allow empty value if location is setted.

## Version 1.2

#### Release date: April 9th, 2015

 - Adding AppNexus adNetwork
 - nativeAd improvements
 - Adding [MNGAdsSDKFactory isInitialized]

## Version 1.1.5

#### Release date: March 31th, 2015

 - Timeout improvement
 - Capping improvement (on placementId and not on MNGAdsFactory)
 - Add keyword preferences
 - Bug fix for non arc projects

## Version 1.1.4

#### Release date: March 18th, 2015

 - Update with latest cocoapods
 - timeout improvements

 - https://bitbucket.org/mngcorp/mngads-demo-ios/commits/tag/v1.1.4
## Version 1.1.3

#### Release date: March 11th, 2015

 - Refreshing of ads is now done by mng ads, improving capping functionality and adding debug more

 - https://bitbucket.org/mngcorp/mngads-demo-ios/commits/tag/v1.1.3

## Version 1.1.2

#### Release date: March 6th, 2015

 - Add support for badge view in native ads (appsfire)

 - https://bitbucket.org/mngcorp/mngads-demo-ios/commits/tag/v1.1.2

## Version 1.1.1

#### Release date: March 5th, 2015

 - Update Google Ads to 7.0.0 + Update FacebookAudienceNetwork to 3.23.1 + Removing Crashlytics

 - https://bitbucket.org/mngcorp/mngads-demo-ios/commits/tag/v1.1.1

## Version 1.1

#### Release date: February 10th, 2015

 - Added ```preferredHeight:(CGFloat)preferredHeight``` to more easily resize banners.


## Version 1.0

#### Release date: December 23th, 2014

 - Initial version

---
[Upgrade Guide]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/upgrading
[MngAdsSDK]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/
[BlueStack-SDK]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/
[GoogleMobileAds.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/Google-Mobile-Ads-SDK/?at=master
[Design Guidelines and Best practices]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/guidelines
[Wiki]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/
[Help Center]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/faq
[LiveRailSDK.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/AdsSDKs/LiveRailSDK.framework/?at=master
[libFlurryAds]:https://github.com/flurry/ios-AdIntegrationSamples/tree/master/Pods/Flurry-iOS-SDK
[libFlurry]:https://github.com/flurry/ios-AdIntegrationSamples/tree/master/Pods/Flurry-iOS-SDK
[Interstital implementation]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Home#markdown-header-interstitial
[mnAds Adapters]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Pods/MNGAds/MNGAds/?at=master
[In-Feed Ad format]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Home#markdown-header-infeed
[App Transport Security]:https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW60
[debug-mode-gyro]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/debug-mode-gyro
[BeaconForStoreSDK.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/d41507a6c8eac3829efd9b05247acac1fcc51f8f/Demo/MNG-Ads-SDK/BeaconForStoreSDK.framework/?at=master
[umoove.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/Umoove.framework/?at=master
[Rewarded Video for iOS]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/rewarded-video-ios
[nativead format]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/nativead

[libSmartAdServer.a]:http://help.smartadserver.com/en/#../../../../specifications/Content/MobileSpecifications/Apps.htm
[FBAudienceNetwork.framework]:https://developers.facebook.com/docs/audience-network/download
[GoogleMobileAds.framework]:https://developers.google.com/mobile-ads-sdk/docs/dfp/ios/download
[GoogleMobileAds.xcframework]:https://developers.google.com/mobile-ads-sdk/docs/dfp/ios/download
[AmazonAd.framework]:https://developer.amazon.com/sdk-download
[libFlurryAds.a]:https://github.com/flurry/ios-AdIntegrationSamples/tree/master/Pods/Flurry-iOS-SDK
[libFlurry.a]:https://github.com/flurry/ios-AdIntegrationSamples/tree/master/Pods/Flurry-iOS-SDK
[MoPub Marketplace]: https://github.com/mopub/mopub-ios-sdk
[libMAdvertiseMoPubAdapter.a]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/
[Native Ad Choice position]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/nativead#markdown-header-native-ad-adchoice
[Vectaury.framework]:https://cdn.vectaury.io/static/sdk/
[AdColony.framework]:https://github.com/AdColony/AdColony-iOS-SDK-3
[libSmartAdServer.a]:http://help.smartadserver.com/en/#../../../../specifications/Content/MobileSpecifications/Apps.htm
[GDPR]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/gdpr
[MAdvertiseVectaury]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/MAdvertiseVectaury
[OMSDK_Madvertise-x.framework]:https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/OMSDK_Madvertise-1.2.4.framework.zip
[MAdvertiseLocation-v1.0]: https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/MAdvertiseLocation-v1.0.zip
[MAdvertiseLocation]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/MadvertiseLocation
[MAdvertiseLocation-v1.1]: https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/MAdvertiseLocation-v1.1.zip
[MAdvertiseLocation-v1.3]: https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/MAdvertiseLocation-v1.3.zip
[MAdvertiseLocation-v1.2]: https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/MAdvertiseLocation-v1.2.zip
[MAdvertiseLocation-v1.4]: https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/MAdvertiseLocation-v1.4.zip
[MAdvertiseLocation-v1.6]: https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/MAdvertiseLocation-v1.4.zip
[MAdvertiseLocation-v1.6]: https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/MAdvertiseLocation-v1.6.zip
[MAdvertiseLocation-v1.7]: https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/MAdvertiseLocation-v1.7.zip
[MAdvertiseLocation-v1.8]: https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/MAdvertiseLocation-v1.8.zip
[MAdvertiseLocation-v1.9]: https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/MAdvertiseLocation-v1.9.zip
[MAdvertiseLocation-v2.0]: https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/MAdvertiseLocation-v2.0.zip
[MAdvertiseLocation-v2.1.1]: https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/MAdvertiseLocation-v2.1.1.zip
[MAdvertiseLocation-v2.2]: https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/MAdvertiseLocation-v2.2.zip
[MAdvertiseLocation-v2.3]: https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/MAdvertiseLocation-v2.3.zip
[MAdvertiseLocation-v2.3.1]: https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/MAdvertiseLocation-v2.3.1.zip
[MAdvertiseLocation-v3.0.0] : https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/MAdvertiseLocation-v3.0.0.zip

[(more infos)]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/Home#markdown-header-disable-auto-displaying

[Thumbnail Ads]:https://bitbucket.org/mngcorp/mngads-demo-ios/wiki/thumbnail
[BlueStack-SDK-Core]: https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/Bluestack-SDK-Core-v3.2.3.zip