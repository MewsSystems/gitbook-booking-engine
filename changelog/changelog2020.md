# Changelog 2020

## 26th November 2020

* API: Changed of [API Client Authorization](./authorization.md). Where the client needs to be registered.

## 20th November 2020

* API: Made `ConfigurationId` parameter in [Create reservation group](./operations.md#create-reservation-group) endpoint required.
* API: Added `ConfigurationId` parameter to [Get availability](./operations.md#get-availability) endpoint.
* API: Previous variant of sending `HotelId` without `ConfigurationId` to these endpoints was deprecated.
* Standalone: Stopped support for hotel/enterprise ids in URL and in the configuration of a javascript client.
* Standalone: Configuration ids are now the only supported way to setup Distributor.

## 28th August 2020

* API: Added `CurrencyCode` parameter to [Get availability](./operations.md#get-availability) endpoint.

## 22nd June 2020

* API: Added section describing payment card support.
* API: Improved `PaymentGatewayData` description.
* API: Removed deprecated payment gateways.
* API: Improved `CreditCardData` description.
* API: [PR 36](https://github.com/MewsSystems/gitbook-distributor-guide/pull/36/files)
* Widget: Updated info about payment gateways and payment card storages. 
* Widget: [PR 36](https://github.com/MewsSystems/gitbook-distributor-guide/pull/36/files)

## 18th June 2020

* API: Removed `AlwaysIncluded` field from [Product](./operations.md#product) \([37](https://github.com/MewsSystems/gitbook-distributor-guide/pull/37/files)\). In order to pre-select a product during a booking, you can use `IncludedByDefault` field.

## 22nd April 2020

* API: Added following sections: Configuration, Theme, City, PaymentCardInput, RequiredField, Enterprise and Address.

## 23rd March 2020

* Widget: Added guide for conditionally firing tags based on tracking consents.

## 20th March 2020

* Widget: Added tracking consents integration.

## 18th March 2020

* API: Added `close()` FE api description.

## 4th March 2020

* API: Added SendMarketingEmail field to Booker.

## 3rd March 2020

* API: Added enums for RateGroups section and some minor improvements.

## 26th February 2020

* API: Added documentation for `hotels/getPaymentConfiguration`.
* API: Deleted old/legacy `payments/getPaymentGateway`.
