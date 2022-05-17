# Google Triggers Reference

> **Notice of usage:** Google Tag Manager is a third party service and we provide this integration as is. We export a set of supported events and their data to the container, however, we have no control over what happens to them and how they are used. Below we provide a set of basic setup examples that have been tested and verified to work with the Mews Booking Engine. If you need a more complex setup, it is up to you to configure and test it.

All events data is passed to Tag Manager through _Data Layer_. To use it in your tags, set up _Variable_ with a proper name as a variable of the data layer, like this:

![variable](../../.gitbook/assets/variable.png)

> **Note:** All prices currently presented via the data layer are gross \(including taxes and fees\)

### Data layer variables in events

Each event is fired with a standard set of data:

| Data Layer Variable Name | Description |
| :-- | :-- |
| eventName | Name of the event in readable form without prefix, e.g. `Step Dates`. |
| trackingConsents | [TrackingConsents](#trackingconsents) applied at the time the event was created. |

If a hotel is selected, information about it is also added to the event \(note the hotel is always selected when in _Singlehotel_ mode\).

| Data Layer Variable Name | Description |
| :-- | :-- |
| hotelName | Name of the hotel |
| hoteId | Unique identifier of the hotel |

Some events expose additional data layer variables. They are described separately for each event.

### TrackingConsents

| Name | Type | Contract | Purpose |
| :-- | :-- | :-- | :-- |
| advertising | boolean | required | Advertising, e.g. used to help advertisers deliver more relevant advertising, or to limit how many times you see an advertisment. |
| functional | boolean | required | Unnecessary functionality, e.g. remembering user choices made in the past. |
| necessary | boolean | required | Necessary functionality. |
| performance | boolean | required | Performance, e.g. collecting information about how users use a website; data are anonymized. |

### distributorLoaded   <a id="distributorloaded"></a>

The Distributor application was initialized \(triggers once per session even with a Merchant redirect\).

### distributorConfigurationSet   <a id="distributorconfigurationset"></a>

Initial values were configured. When there is no custom value, it propagates the default one.

| Data Layer Variable Name | Description |
| :-- | :-- |
| startDate | Start date in ISO 8601 format YYYY-MM-DD, i.e.`2017-01-20`. |
| endDate | End date in ISO 8601 format YYYY-MM-DD, i.e.`2017-01-22`. |
| languageCode | Language code, i.e. `en-US`. |
| currencyCode | Currency code in ISO format, i.e`EUR` |
| promoCode | Value of the promo code, i.e.`promo`. |

### distributorOpened

* Booking Engine (Distributor) was opened

### distributorClosed

* Booking Engine (Distributor) was closed

### distributorTrackingConsentsSet

* [TrackingConsents](#trackingconsents) were set

### distributorStepDates

* A Dates step was displayed

### distributorStepHotels

* A Hotels step was displayed

### distributorStepRooms

* A Rooms step was displayed

### distributorStepRates

* A Rates step was displayed

### distributorStepSummary

* A Summary step was displayed

### distributorStepCheckout

* A Checkout step was displayed

### distributorStepConfirmation

* A confirmation page was displayed

### distributorLanguageCodeChanged

* A language code was changed

| Data Layer Variable Name | Description |
| :-- | :-- |
| languageCode | Language code of the selected language, e.g. `en-US`. |

### distributorCurrencyCodeChanged

* A currency code was changed

| Data Layer Variable Name | Description |
| :-- | :-- |
| currencyCode | Currency code of the selected currency, e.g. `USD`. |

### distributorStartDateSelected

* A start date of the reservation was selected

| Data Layer Variable Name | Description |
| :-- | :-- |
| startDate | Selected start date in ISO 8601 format YYYY-MM-DD, e.g. `2017-01-20`. |

### distributorEndDateSelected

* An end date of the reservation was selected

| Data Layer Variable Name | Description |
| :-- | :-- |
| endDate | Selected end date in ISO 8601 format YYYY-MM-DD, e.g.`2017-01-22`. |

### distributorPromoCodeSelected

* A promo code was set

| Data Layer Variable Name | Description |
| :-- | :-- |
| promoCode | Value of the inserted promo code as a string, e.g. `promo`. It is not validated. |

### distributorAvailabilityLoaded

* Availability of hotel was loaded

| Data Layer Variable Name | Description |
| :-- | :-- |
| availableRooms | Array of available rooms or spaces. |

* Each item in the `availableRooms` array contains the following data:

| Name | Description |
| :-- | :-- |
| roomName | Name of the room or space. |
| roomId | Unique identifier of the room or space. |
| availableRateIds | List of available rate ids for the room or space |
| lowestPrice | Price of the room or space in the hotel's default rate currency |
| price | All prices of the room or space in all available currencies as `(key: currency, value: price)` dictionary/object. |

### distributorAlternativeDatesOffered

* Alternative dates were displayed

### distributorOfferedDatesSelected

* Alternative dates when there is no availability selected

### distributorCategoryGalleryOpened

* Category gallery was opened

### distributorRoomSelected

* A room or space was selected

| Data Layer Variable Name | Description |
| :-- | :-- |
| roomId | Unique identifier of the selected room or space. |
| roomName | Name of the selected room or space in the hotel’s default language. |
| spaceType | Name of the space type (`Room`, `Bed` or `Dorm`) for the selected room or space. |

### distributorSpaceTypeCountChanged

* The count of the selected space type was changed

| Data Layer Variable Name | Description |
| :-- | :-- |
| count | Count of the selected space type. |

### distributorRoomOccupancyChanged

* The count of adults and/or children was changed for the room or space

| Data Layer Variable Name | Description |
| :-- | :-- |
| roomIndex | Index of the changed room or space. |
| adultCount | Number of the selected adults. |
| childCount | Number of the selected children. |

### distributorProductAdded

* A product was added to the order

| Data Layer Variable Name | Description |
| :-- | :-- |
| productId | Unique identifier of the added product. |
| productName | Name of the product in the hotel’s default language. |

### distributorProductRemoved

* A product was removed from the order

| Data Layer Variable Name | Description |
| :-- | :-- |
| productId | Unique identifier of the removed product. |
| productName | Name of product in the hotel’s default language. |

### distributorRoomAdded

* A room or rooms were added to the order

| Data Layer Variable Name | Description |
| :-- | :-- |
| reservations.orderId | Unique identifier used only within session to identify order items |
| reservations.hotelId | Unique identifier of selected hotel |
| reservations.roomId | Unique identifier of selected room or space |
| reservations.rateId | Unique identifier of selected rate |
| reservations.productIds | Collection of selected product unique identifiers |
| reservations.startDate | Reservation start date |
| reservations.endDate | Reservation end date |
| reservations.adultCount | Number of selected adults |
| reservations.childCount | Number of selected children |

### distributorRoomCountChanged

* The quantity of rooms or spaces in the order was increased or decreased

| Data Layer Variable Name | Description |
| :-- | :-- |
| orderId | Unique ID used only within session to identify order items |
| roomId | Unique identifier of selected room or space |
| rateId | Unique identifier of selected rate |
| countChange | Change of quantity \(e.g. 1, -1\) |

### distributorBookingPrepared

* A booking is prepared and user needs to enter their details; this event triggers when the user reaches the Checkout step

| Data Layer Variable Name | Description |
| :-- | :-- |
| totalCost | current total cost of the reservation group, in the hotel’s default currency |

### distributorBookingFinished

* A booking was made; this event triggers once every time a reservation group is made

| Data Layer Variable Name | Description |
| :-- | :-- |
| reservationGroupId | ID of the reservation group |
| totalCost | Total cost of the reservation group, in the hotel’s default currency |
| currencyCode | Hotel’s default currency code in ISO format |

### distributorReservationCreated

* A reservation was created; this event triggers when each reservation is made in the reservation group

| Data Layer Variable Name | Description |
| :-- | :-- |
| customerEmail | The customer’s email |
| customerName | The customer’s name |
| currencyCode | Hotel’s default currency code in ISO format |
| reservationGroupId | ID of the reservation group |
| id | ID of the reservation |
| roomId | ID of the room or space category |
| rateId | ID of the rate of the reservation |
| number | Confirmation number of the reservation |
| roomName | Name of the room or space |
| startDate | Start date of the reservation |
| endDate | End date of the reservation |
| nights | Total number of nights |
| cost | Cost of the reservation in the hotel’s default currency |
| alternativeCost | Cost of the reservation in all currencies supported by the property as \(key: currency, value: price\) dictionary/object. |
