# upgrading SDK

## Upgrading to v1.4

Now appNexus is available on Cocoapods and pod generate libAppNexusSDK.a, you must remove libANSDK.a old librairy in order to avoid duplicate symbol.

## Upgrading to v1.3.2

The call to the following methods 

```
#!objective-c
-(BOOL)createInterstitialWithPreferences:(MNGPreference*)preferences autoDisplayed:(BOOL)autoDisplyed;  
-(BOOL)createInterstitialAutoDisplayed:(BOOL)autoDisplyed;
```

should be replaced by

```
#!objective-c
-(BOOL)createInterstitialWithPreferences:(MNGPreference*)preferences;
-(BOOL)createInterstitial;
```

## Upgrading to v1.2.1

Bug preference.keyword, now allow empty value if location is setted.

## Upgrading to v1.2

You must add **Appnexus** library. You must setpreference.keyword,if location is setted.(bug fix in v1.2.1)

## Upgrading from v1.0 to v1.1

The following methods have been changed. ```preferredHeight:(CGFloat)preferredHeight``` is now available to more easily resize banners.


```
#!objective-c

(void)adsAdapter:(MNGAdsAdapter *)adsAdapter bannerDidLoad:(UIView *)bannerView preferredHeight:(CGFloat)preferredHeight{
```


instead of


```
#!objective-c

(void)adsAdapter:(MNGAdsAdapter *)adsAdapter bannerDidLoad:(UIView *)bannerView{
```




