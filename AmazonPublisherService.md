#Amazon Publisher Service

##Installation

* ***CocoaPods installation*** :

Installation with MNGSDK V2.14 (since v2.14)
You must download manually [DTBAmazonAps](https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/DTBiOSSDK.zip) and you will need to specify the subspec for "AmazonAps" since it s not included by default like so :

1. Go to [DTBAmazonAps](https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/DTBiOSSDK.zip)
2. Drag and drop it in your project.
3. Run pod command

```
  pod "MNGAds",:subspecs => ["MNGAdsFull", "AmazonAps"]

```
* ***Manual  installation*** : 


1. Go to [DTBAmazonAps](https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/DTBiOSSDK.zip)
2.  drag and drop it in your project.

3.  You must add to your project  libMNGAmazonAPSAdapter.a the adNetwork SDK also (inside the folder of MNGAds) .