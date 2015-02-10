# upgrading SDK

## Upgrading from 1.0 to 1.1

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




