# Changelog 2020

## 26th November 2020

* Changed of [API Client Authorization](./authorization.md). Where the client needs to be registered.

## 20th November 2020

* Made `ConfigurationId` parameter in [Create reservation group](./operations.md#create-reservation-group) endpoint required.
* Added `ConfigurationId` parameter to [Get availability](./operations.md#get-availability) endpoint.
* Previous variant of sending `HotelId` without `ConfigurationId` to these endpoints was deprecated.

## 28th August 2020

* Added `CurrencyCode` parameter to [Get availability](./operations.md#get-availability) endpoint.

## 22nd June 2020

* Added section describing payment card support.
* Improved `PaymentGatewayData` description.
* Removed deprecated payment gateways.
* Improved `CreditCardData` description.
* [PR 36](https://github.com/MewsSystems/gitbook-distributor-guide/pull/36/files)

## 18th June 2020

* Removed `AlwaysIncluded` field from [Product](./operations.md#product) \([37](https://github.com/MewsSystems/gitbook-distributor-guide/pull/37/files)\). In order to pre-select a product during a booking, you can use `IncludedByDefault` field.

## 22nd April 2020

* Added following sections: Configuration, Theme, City, PaymentCardInput, RequiredField, Enterprise and Address.

## 18th March 2020

* Added `close()` FE api description.

## 4th March 2020

* Added SendMarketingEmail field to Booker.

## 3rd March 2020

* Added enums for RateGroups section and some minor improvements.

## 26th February 2020

* Added documentation for `hotels/getPaymentConfiguration`.
* Deleted old/legacy `payments/getPaymentGateway`.
