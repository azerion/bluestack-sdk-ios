# upgrading SDK

## Upgrading to v1.2

You must add **Appnexus** library.

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




