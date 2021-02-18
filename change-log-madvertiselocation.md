Change log and release notes for MadvertiseLocation for iOS.

### Version 2.3.1
#### Release date: February 18th, 2021

* Fix compilation issue on Swift project ("Failed to build module 'MAdvertiseLocation' from its module interface; it may have been damaged or it may have triggered a bug in the Swift compiler when it was produced")

### Version 2.3
#### Release date: February 8th, 2021

* Swift version 5.3.2 and Xcode 12.4

### Version 2.2
#### Release date: October 31th, 2020

 - fix IDFA and CMP issue

### Version 2.1.1
#### Release date: October 6th, 2020
* **Xcode 12.0.1 + target on Swift 5.x**
* fix Xcode 12.0.1 compilation issue.

### Version 2.1
#### Release date: September 30th, 2020
* **Xcode 12 + target on Swift 5.x**
* fix iOS 14 accuracy.
* **IMPORTANT add new key in plist for prompt reduced accuracy by default** : 
```
#!xml


<! -- info.plist -->
<key>NSLocationDefaultAccuracyReduced<\key><true/>
```


### Version 2.0
#### Release date: September 16th, 2020
* TCF v2 support.
* fix iOS 10 crashes.

### Version 1.9
#### Release date: july 23th, 2020

 - Implemented  new Init MadvertiseBuilder with new attribute consent flag 

case consentFlag = "0" = user do not allow
case consentFlag = "1" = user provide consent
case consentFlag = "2" = SDK must check consent IAB consent
case consentFlag = "3" = SDK must check Madvertise consent



### Version 1.8
#### Release date: March 27th, 2020

 - Xcode 11.4 + target on Swift 5.x



### Version 1.7
#### Release date: December 16th, 2019

 - Loc-CheckConsent - header

### Version 1.6
#### Release date: September 18th, 2019

 - Xcode 11 and iOS13 support
 - use UTC timezone for all events

### Version 1.5
#### Release date: September 3th, 2019

 - A MESSAGE THAT TELLS THE USER WHY THE APP IS REQUESTING ACCESS TO THE USER’S LOCATION INFORMATION WHILE THE APP IS RUNNING IN THE FOREGROUND 

### Version 1.4
#### Release date: May 3th, 2019

 - Optimize number of points per day (recurency)
 - Date optimization

### Version 1.3
#### Release date: April 1th, 2019

 - Support Xcode 10.2
 - Migrate to swift 5
 - Manage MadvertiseConsent_ConsentString (specific purposes for GPS data) from CMP that replace IABConsent_LocationPurpose
 - Allow debug Mode

### Version 1.2
#### Release date: March 19th, 2019

 - Manage IABConsent_LocationPurpose from CMP
 - migrate to swift 5

### Version 1.1
#### Release date: February 1th, 2019

 - fix crash checkBetweenLastDateSavedAndLastDateSended

### Version 1.0
#### Release date: December 12th, 2018

 - initial release