#Madvertise Location SDK


* ### Prerequisites
 
    * ##### A message that tells the user why the app is requesting access to the user’s location at all times:

         * From iOS 10, set “NSLocationAlwaysUsageDescription” and “NSLocationWhenInUseUsageDescription” in the Info.plist file.
         * From iOS 11, set “NSLocationAlwaysAndWhenInUseUsageDescription” and “NSLocationWhenInUseUsageDescription” in the Info.plist file.

    * ##### A message that tells the user why the app is requesting access to the user’s location information while the app is running in the foreground. **(Since madvertiseLocation V1.5)** :


         * From iOS 10, set “NSLocationWhenInUseUsageDescription” in the Info.plist file.

         * from IOS 14 
 prompt for reduced accuracy by default : 

```
#!xml


<! -- info.plist -->
<key>NSLocationDefaultAccuracyReduced<\key><true/>
```




*  ##  Installation   :
https://bitbucket.org/mngcorp/mngads-demo-android/wiki/change-log-madvertiselocation
* ***CocoaPods installation*** :  

## Installation with MNGSDK V2.3.1 (since v2.12.1)
You will just need to specify the subspec for Madvertise Location since it s not included by default like so :

```
  pod "MNGAds",:subspecs => ["MNGAdsFull", "MAdvertiseLocation"]
```

 ===> the functions of madevertiselocation will work automatically after the Init of mngads 
## Installation Without MNGSDK
```
#!Podfile

use_frameworks! 
pod 'MAdvertiseLocation'
```



* ***Manually  installation*** : 

1. Go to [MAdvertiseLocation-vx](https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/)

2. Select the project file from the project navigator on the left side of the project window.

3. Select the target for where you want to add frameworks in the project settings editor.

4. Select the “Build Phases” tab, and click the small triangle next to “Link Binary With Libraries” to view all of the frameworks in your application.

5. To Add frameworks, click the “+” below the list of frameworks.



# Integration #

* **Enable Background Mode**
You need to tick the box "Location updates" in the "Capabilities" of your target.

![Capabilities.png](https://bitbucket.org/repo/aen579/images/3460637221-Capabilities.png)


** That for  use  in standalone without the mngads SDK :** 


1.**requestAuthorization** :

Ask the user to share their location data (popup) with the +requestAuthorization: function:
 Put this line where it makes the most sense for your app user experience. This will trigger a permission request popup. If you already asked thoses permissions elsewhere in your app, you don't need to call it (if you do, it will have no impact).




```
#!objective-c

        [MAdvertiseLocation madvertiseLocationRequestAuthorization ];

```


```
#!Swift

        MAdvertiseLocation.madvertiseLocationRequestAuthorization()

```


2.**Initializing MAdvertiseLocation**


```
#!objective-c

         MadvertiseBuilder * madvertiseBuilder = [[MadvertiseBuilder alloc] init];
        [madvertiseBuilder setWithAppId:madevertiseLocationKey];
```

```
#!Swift

        let madvertiseBuilder:MadvertiseBuilder? =  MadvertiseBuilder()
        madvertiseBuilder?.set(appId: ConfigurationFile.madervertiseLocationAppId)
        let madvertiseLocationContext: MAdvertiseLocation? = madvertiseBuilder?.build()

```
 ***(since v1.9) new attribute Consent flag passed to init madvertiseBuilder :***
 
 * case consentFlag =  "0" = user do not allow  
 * case consentFlag =  "1" = user provide consent
 * case consentFlag =  "2" = SDK must check consent IAB consent
 * case consentFlag =  "3" = SDK must check Madvertise consent

 
```
#!objective-c

        [madvertiseBuilder setWithConsentFlag:@"0"];
```

```
#!Swift

        madvertiseBuilder?.set(consentFlag: consentFlag)
        

```
 

3.**Start Location tracking position** :
Start to collect location data with start function:


```
#!objective-c

 [MAdvertiseLocation startWithMadvertiseLocation:madlocation];

```
```
#!Swift
  MAdvertiseLocation.start(madvertiseLocation:madvertiseLocationContext!)

```