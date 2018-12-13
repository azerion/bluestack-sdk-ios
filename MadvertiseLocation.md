#Madvertise Location SDK

Installation:
You will just need to specify the subspec for Madvertise Location since it s not included by default like so:

  pod "MNGAds",:subspecs => ["MNGAdsFull", "MAdvertiseLocation"]

Also you need to make sure to add their Settings.bundle after the installation is complete 

* **requestAuthorization** :

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

* **Enable Background Mode**
You need to tick the box "Location updates" in the "Capabilities" of your target.

![Capabilities.png](https://bitbucket.org/repo/aen579/images/3460637221-Capabilities.png)

* **Initializing MAdvertiseLocation**
Once the installation has been successful you will need to initialise 



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

* **Start Location tracking position** :
Start to collect location data with start function:


```
#!objective-c

 [MAdvertiseLocation startWithMadvertiseLocation:madlocation];

```
```
#!Swift
  MAdvertiseLocation.start(madvertiseLocation:madvertiseLocationContext!)

```