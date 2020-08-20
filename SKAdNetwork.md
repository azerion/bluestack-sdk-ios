# Enable SKAdNetwork to track conversions

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