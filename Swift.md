# Installation guide for Swift

In order to use the BlueStack SDK in your Swift based application, you'll need to go through a few additional steps:

You have to import BlueStack SDK's headers in your Bridging-Header.h

```
#import "MNGAdsSDKFactory.h"
#import "Protocols.h"
#import "MNGNAtiveObject.h"
#import "MNGPreference.h"

```

If you don't have a Bridging-Header.h, you have to create a one. (steps: [Objective-C bridging header](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/BuildingCocoaApps/MixandMatch.html#//apple_ref/doc/uid/TP40014216-CH10-XID_78))

After that you can use BlueStack SDK in your Swift file. (example: [SwiftViewController.swift](https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/SwiftViewController.swift?at=master))


Or  that you can use BlueStack SDK in your Swift Project. (Demo Swift : [Demo Swift](https://bitbucket.org/mngcorp/mngads-demo-ios/src/HEAD/Demo/MNG-Ads-SDK/SwiftViewController.swift?at=master))

[Demo Swift](https://bitbucket.org/mngcorp/mngads-demo-ios/src/master/DemoSwift/)
# Error Handling : 

if you have this error log : 

```
‼️MNGMngPerfAdapter not found
```

 Do not forget to include the "-ObjC " and " -l"BlueStack" " linker flag in "Other Linker Flags" under "Build Settings" in the project file.

