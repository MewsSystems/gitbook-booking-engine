# Changelog 2021

## 29th November 2021

* Changed domain from www.mews.li to api.mews.com
 
## 9th November 2021

* Added [CategoryImageAssignment](./operations.md#category-image-assignment) docs and [deprecated ImageIds in the RoomCategory](./deprecations/README.md).

## 3rd August 2021

* Added `AverageAmountPerTimeUnit` field to [Room price](./operations.md#room-price) replacing the `AverageAmountPerNight`.
* Added `ChargingMode` field to [Product](./operations.md#product) replacing the `Charging`.
* Added `PostingMode` field to [Product](./operations.md#product) replacing the `Posting`.
* Added `SettlementMaximumTimeUnits` field to [Rate group](./operations.md#rate-group) replacing the `SettlementMaximumNights`.

## 21st July 2021

* Added `Services` parameter at [Get configuration](./operations.md#get-configuration) endpoint that uses newly added [Service](./operations.md#service) object.

## 10th May 2021

* Fixed inconsistency in naming in the documentation.
* Fixed DTOs table heading to reflect the columns.

## 3rd May 2021

* Added use case on [On session payment card authorization](./use-cases/on-session-payment-card-authorization.md).

## 19th April 2021

* Moved use case on [How to support payment card in booking engine client application](./use-cases/how-to-support-payment-cards-in-booking-engine-application.md).

## 30th March 2021

* Added use case for [On session payments](./use-cases/on-session-payments.md).

## 25th March 2021

* Changed naming of URL variables used in the documentation to make clear distinction between application URLs and API URLs.

## 19th March 2021

* Changed urls for testing (demo) environments.

| Next |
| :-- |
| [Changelog 2020](changelog2020.md) |
