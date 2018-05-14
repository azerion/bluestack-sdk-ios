# GDPR

# GDPR

The GDPR (General Data Protection Regulation) is a set of rules within the EU law that regulates the use and process of the consumer's personal data.
The new General Data Protection Regulation law will apply in Europe starting 25th May 2018. It will provide the custumers with more protection over their personal informations by making companies more responsable about the way they interact them.

MAdvertise participates as a vendor in [IAB Europe’s Transparency & Consent Framework].

MAdvertise provides a method with which the publisher will determine whether GDPR scope applies to the app or user / device and if applicable, capture end user consent in [IAB EU Transparency Consent Framework] format.

Publishers are free to implement or develop the CMP of their choice as long as the consent management is based on the IAB Transparency & Consent Framework. [Here] is the list of currently available registered CMPs.

Apps should provide wether they are in the GDPR scope, and if so the consent strings.
More informations in the [GDPR Consent Demo]).

Usage example of MAdvertiseConsent
```objc

MAdvertiseConsent *consent = [[MAdvertiseConsent alloc]initWithGDPRScope:true.on andConsentStrings:@{@"IAB":"BONlRnIONlRnIAAABAENAAAAAAAAoAA"}];
[MAdvertiseConsent setConsentInformation:consent];
// please check out the MAdvertiseConsent header file more information
```

`Notes`:  For now, end user consent string must be passed with key name IAB. Anything else will be ignored.

[GDPR Consent Demo]:https://quantcast.mgr.consensu.org/index.html](https://quantcast.mgr.consensu.org/index.html
[IAB EU Transparency Consent Framework]: http://advertisingconsent.eu/
[Here]: http://advertisingconsent.eu/iab-europe-transparency-consent-framework-list-of-registered-cmps/
[IAB Europe’s Transparency & Consent Framework.]:http://advertisingconsent.eu/transparency-consent-framework-global-vendor-list/