# Prepare for iOS 14+
[TOC]

## Request App Tracking Transparency authorization

To display the App Tracking Transparency authorization request for accessing the IDFA, update your Info.plist to add the NSUserTrackingUsageDescription key with a custom message describing your usage. Below is an example description text:


```
#!objective-c

<key>NSUserTrackingUsageDescription</key>
<string>This identifier will be used to deliver personalized ads to you.</string>
```

![editor.png](https://bitbucket.org/repo/aen579/images/4098905308-editor.png)

![att-iOS.png](https://bitbucket.org/repo/aen579/images/2434364878-att-iOS.png)

To present the authorization request, call requestTrackingAuthorizationWithCompletionHandler:. We recommend waiting for the completion callback prior to loading ads, so that if the user grants the App Tracking Transparency permission, the BlueStack-SDK can use the IDFA in ad requests.


```
#!swift

import AppTrackingTransparency
import AdSupport
...
func requestIDFA() {
  ATTrackingManager.requestTrackingAuthorization(completionHandler: { status in
    // Tracking authorization completed. Start loading ads here.
    // loadAd()
  })
}
```


```
#!objective-c

#import <AppTrackingTransparency/AppTrackingTransparency.h>
#import <AdSupport/AdSupport.h>
...
- (void)requestIDFA {
  [ATTrackingManager requestTrackingAuthorizationWithCompletionHandler:^(ATTrackingManagerAuthorizationStatus status) {
    // Tracking authorization completed. Start loading ads here.
    // [self loadAd];
  }];
}
```



For more information about the possible status values, see [ATTrackingManager.AuthorizationStatus].

## Enable SKAdNetwork to track conversions

The BlueStack-SDK supports conversion tracking using [Apple's SKAdNetwork], which means BlueStack is able to attribute an app install even when IDFA is unavailable.

To enable this functionality, you will need to update the SKAdNetworkItems key with an additional dictionary in your Info.plist.


```
#!plist


<key>SKAdNetworkItems</key>
  <array>
    <dict>
      <key>SKAdNetworkIdentifier</key>
      <string>PD25VRRWZN.skadnetwork</string>
    </dict>
  </array>
```

  


[Apple's SKAdNetwork]:https://developer.apple.com/documentation/storekit/skadnetwork
[ATTrackingManager.AuthorizationStatus]:https://developer.apple.com/documentation/apptrackingtransparency/attrackingmanager/authorizationstatus