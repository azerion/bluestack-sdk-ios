### MAdvertiseBeacon

- Get Ebeacon technology to propose to the advertisers to target the users inside the point of sale.
- An installation base of 12,500 ebeacons ready to track the users.
- An exclusive format in Push notification to the users inside a tabacco shop, press shop, pharmay or mall.

### Initializing Beacons
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