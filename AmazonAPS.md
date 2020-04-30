#Amazon APS 

##Installation

* ***CocoaPods installation*** :

Installation with MNGSDK V2.14 (since v2.14)
You will just need to specify the subspec for "AmazonAps" since it s not included by default like so :


```
  pod "MNGAds",:subspecs => ["MNGAdsFull", "AmazonAps"]

```
* ***Manual  installation*** : 


1. Go to [DTBAmazonAps](https://bitbucket.org/mngcorp/mngads-demo-ios/downloads/DTBiOSSDK.zip)

2.  drag and drop it in your project (inside the folder of MNGAds).

3.  You must add to your project  libMNGAmazonAPSAdapter.a the adNetwork SDK also (inside the folder of MNGAds).