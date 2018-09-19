# Installation guide for Swift

In order to use the MNGAds SDK in your Swift based application, you'll need to go through a few additional steps:

You have to import MNGAds SDK's headers in your Bridging-Header.h

```
#import "MNGAdsSDKFactory.h"
#import "Protocols.h"
#import "MNGNAtiveObject.h"
#import "MNGPreference.h"
```

If you don't have a Bridging-Header.h, you have to create a one. (steps: [Objective-C bridging header](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/BuildingCocoaApps/MixandMatch.html#//apple_ref/doc/uid/TP40014216-CH10-XID_78))

After that you can use MNGAds SDK in your Swift file. (example: [SwiftViewController.swift](https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/SwiftViewController.swift?at=master))


## GDPR

Following code must be used in order to send consentString from CMP

```
let consentDict = ["IAB":"consentString"]
let consent = MAdvertiseConsent(gdprScope: true, andConsentStrings: consentDict)
MAdvertiseConsent.setConsentInformation(consent)
```