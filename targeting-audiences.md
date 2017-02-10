# Targeting Audiences

[TOC]

In order to take advantage of our targeting campaign, you must use our **Preferences object**.


```
#!objective-c
MNGPreference * preference = [[MNGPreference alloc]init];
```



## Location Targeting

**The Madvertise adserver and certain ad can use your user’s location to send more targeted ads by passing Latitude and Longitude.**

You must also edit the **plist** by adding **NSLocationAlwaysUsageDescription** key.

>your application can be rejected by Apple if you use the device's location only for advertising

```
#!objective-c

if (![APP_DELEGATE sharedLocationManager]) {
        APP_DELEGATE.sharedLocationManager = [[CLLocationManager alloc]init];
        if([[APP_DELEGATE sharedLocationManager]respondsToSelector:@selector(requestWhenInUseAuthorization)]) {
            [APP_DELEGATE.sharedLocationManager requestWhenInUseAuthorization];
        }
        [APP_DELEGATE.sharedLocationManager startUpdatingLocation];
    }
preferences.location = [APP_DELEGATE sharedLocationManager].location;
```

>this link can help you to get [device location].


## Keyword Targeting

Keywords allow you to target certain ad requests with user data. Keywords are useless for targeting, if you can provide **dynamic values** per users/devices.

To add keyword targeting, you will need to pass these keywords up through the application (They should be formatted as key/value pairs) :

```
#!objective-c

preference.keyword = @"page=football;category=sport";//Separator in case of multiple entries is ; key=value
```

Target campaigns using the keyword targeting function on Madvertise Console by Madvertise Team.

We can use Positive or Negative targeting

![screenshot-console.mng-ads.com 2017-02-08 14-17-47.png](https://bitbucket.org/repo/aen579/images/3770499640-screenshot-console.mng-ads.com%202017-02-08%2014-17-47.png)


## User demographic Targeting

When people are signed in on your app, can you please share **Demographic informations**  from their settings with following code :

```
#!objective-c
preference.gender = MNGGenderFemale;//or MNGGenderMale
preference.age = 25;//NSInteger

```
Target campaigns with following rules can be apply by Madvertise Team.

 - Age. Target ads to people within an age range.
 - Gender. Target ads to women, men or both.


## Madvertise Audience Targeting

Audiences can be defined by date of birth, gender, locations, Apple's Advertising Identifier (IDFA), Android's advertising ID or by a combination of rules used to identify users who took specific actions on your app (device, carrier, ...).



[device location]:http://www.tutorialspoint.com/ios/ios_location_handling.htm