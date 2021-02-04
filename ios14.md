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

![Image from iOS.png](https://bitbucket.org/repo/aen579/images/3105148460-Image%20from%20iOS.png)

BlueStack-SDK  include App Tracking Transparency (ATT) in order to display the App Tracking Transparency authorization request for accessing the IDFA.


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
        <dict>
            <key>SKAdNetworkIdentifier</key>
            <string>cstr6suwn9.skadnetwork</string>
        </dict>
        <dict>
            <key>SKAdNetworkIdentifier</key>
            <string>v9wttpbfk9.skadnetwork</string>
        </dict>
        <dict>
            <key>SKAdNetworkIdentifier</key>
            <string>n38lu8286q.skadnetwork</string>
        </dict>
        <dict>
            <key>SKAdNetworkIdentifier</key>
            <string>p78axxw29g.skadnetwork</string>
        </dict>
        <dict>
            <key>SKAdNetworkIdentifier</key>
            <string>hs6bdukanm.skadnetwork</string>
        </dict>
        <dict>
            <key>SKAdNetworkIdentifier</key>
            <string>4pfyvq9l8r.skadnetwork</string>
        </dict>
    </array>

```

Up to date list available on following links

* https://madvertise.com/skadnetworkids.xml
* https://madvertise.com/skadnetworkids.json
  


[Apple's SKAdNetwork]:https://developer.apple.com/documentation/storekit/skadnetwork
[ATTrackingManager.AuthorizationStatus]:https://developer.apple.com/documentation/apptrackingtransparency/attrackingmanager/authorizationstatus