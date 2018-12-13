#Madvertise Location SDK


*  ## Installation   :

* ***CocoaPods installation*** :

## Installation:
## Installation with MNGSDK V2.12.1 ##
You will just need to specify the subspec for Madvertise Location since it s not included by default like so :

```
  pod "MNGAds",:subspecs => ["MNGAdsFull", "MadvertiseLocation"]
```


## Installation Without MNGSDK V2.12.1 ##
```
#!Podfile

use_frameworks! 
pod 'MAdvertiseLocation'
```



* ***Manually  installation*** : 

1. Go to [MAdvertiseLocation-v1.0](https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/MAdvertiseLocation-v1.0.zip)

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