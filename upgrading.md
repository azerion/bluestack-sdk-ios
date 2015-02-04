# upgrading SDK

## Upgrading from 1.0 to 1.1

The following methods have been changed. You can use `preferredHeight` as height to have best display for banners


```
#!objective-c

(void)adsAdapter:(MNGAdsAdapter *)adsAdapter bannerDidLoad:(UIView *)bannerView preferredHeight:(CGFloat)preferredHeight{
```


instead of


```
#!objective-c

(void)adsAdapter:(MNGAdsAdapter *)adsAdapter bannerDidLoad:(UIView *)bannerView{
```




