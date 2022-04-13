# Integrations

## Google Tag Manager - Triggers Reference

> ### Notice of usage
> Google Tag Manager is a 3rd party service and we provide this integration as is. We export a set of supported events and their data to the container, however, we have no control over what happens with them and how they are used. Below we provide a set of basic setup examples that have been tested and verified to work with Distributor. If you need a more complex setup, it is up to you to configure and test it.

All events data is passed to Tag Manager through _dataLayer_. To use it in your tags, set up _Variable_ with proper name as a variable of the data layer like this:

![variable](../.gitbook/assets/variable.png)

**All prices currently presented via the data layer are gross \(including taxes and fees\).**

#### Data layer variables in events

Each event is fired with a standard set of data:

| Data Layer Variable Name | Description |
| :--- | :--- |
| eventName | Name of the event in readable form without prefix, i.e.`Step Dates`. |
| trackingConsents | [TrackingConsents](./integrations.md#trackingconsents) applied at the time when event was created. |

If a hotel is selected, information about it is also added to the event. \(Note: The hotel is always selected in the _Singlehotel_ mode\)

| Data Layer Variable Name | Description |
| :--- | :--- |
| hotelName | name of the hotel |
| hoteId | unique identifier of the hotel |

Some events expose additional data layer variables. They are described separately for each event.

#### TrackingConsents

| | Property | Type | Purpose |
| :--- | :--- | :--- | :--- |
| advertising | boolean | required | Advertising, e.g. used to help advertisers deliver more relevant advertising or to limit how many times you see an ad. |
| functional | boolean | required | Unnecessary functionality, e.g. remembering user choices made in the past. |
| necessary | boolean | required | Necessary functionality. |
| performance | boolean | required | Performance, e.g. collecting information about how user uses a website, data are anonymized. |

#### distributorLoaded   <a id="distributorloaded"></a>

The Distributor application was initialized \(triggers once per session even with a Merchant redirect\).

#### distributorConfigurationSet   <a id="distributorconfigurationset"></a>

Initial values were configured. When there is no custom value, it propagates the default one.

| Data Layer Variable Name | Description |
| :--- | :--- |
| startDate | Start date in ISO 8601 format YYYY-MM-DD, i.e.`2017-01-20`. |
| endDate | End date in ISO 8601 format YYYY-MM-DD, i.e.`2017-01-22`. |
| languageCode | Language code, i.e. `en-US`. |
| currencyCode | Currency code in ISO format, i.e`EUR` |
| promoCode | Value of the promo code, i.e.`promo`. |

#### distributorOpened   <a id="distributoropened"></a>

Distributor was opened.

#### distributorClosed   <a id="distributorclosed"></a>

Distributor was closed.

#### distributorTrackingConsentsSet

[TrackingConsents](integrations.md#trackingconsents) were set.

#### distributorStepDates   <a id="distributorstepdates"></a>

A Dates step was displayed.

#### distributorStepHotels   <a id="distributorstephotels"></a>

A Hotels step was displayed.

#### distributorStepRooms   <a id="distributorsteprooms"></a>

A Rooms step was displayed.

#### distributorStepRates   <a id="distributorsteprates"></a>

A Rates step was displayed.

#### distributorStepSummary   <a id="distributorstepsummary"></a>

A Summary step was displayed.

#### distributorStepCheckout   <a id="distributorstepcheckout"></a>

A Checkout step was displayed.

#### distributorStepConfirmation   <a id="distributorstepconfirmation"></a>

A confirmation page was displayed.

#### distributorLanguageCodeChanged   <a id="distributorlanguagecodechanged"></a>

A language code was changed.

| Data Layer Variable Name | Description |
| :--- | :--- |
| languageCode | Language code of the selected language, i.e.`en-US`. |

#### distributorCurrencyCodeChanged   <a id="distributorstartdateselected"></a>

A currency code was changed.

| Data Layer Variable Name | Description |
| :--- | :--- |
| currencyCode | Currency code of the selected currency, i.e.`USD`. |

#### distributorStartDateSelected   <a id="distributorstartdateselected"></a>

A start date of the reservation was selected.

| Data Layer Variable Name | Description |
| :--- | :--- |
| startDate | Selected start date in ISO 8601 format YYYY-MM-DD, i.e.`2017-01-20`. |

#### distributorEndDateSelected   <a id="distributorenddateselected"></a>

An end date of the reservation was selected.

| Data Layer Variable Name | Description |
| :--- | :--- |
| endDate | Selected end date in ISO 8601 format YYYY-MM-DD, i.e.`2017-01-22`. |

#### distributorPromoCodeSelected   <a id="distributorpromocodeselected"></a>

A promo code was set.

| Data Layer Variable Name | Description |
| :--- | :--- |
| promoCode | Value of the inserted promo code as a string, i.e.`promo`. It is not validated. |

#### distributorAvailabilityLoaded   <a id="distributoravailabilityloaded"></a>

Availability of hotel was loaded.

| Data Layer Variable Name | Description |
| :--- | :--- |
| availableRooms | Array of available rooms. |

Each item in the`availableRooms`array contains following data:

| Name | Description |
| :--- | :--- |
| roomName | Name of the room. |
| roomId | Unique identifier of the room. |
| availableRateIds | List of available rate ids for the room |
| lowestPrice | Price of the room in hotel's default rate currency |
| price | All prices of the room in all available currencies as `(key: currency, value: price)` dictionary/object. |

#### distributorAlternativeDatesOffered   <a id="distributoralternativedatesoffered"></a>

Alternative dates were displayed.

#### distributorOfferedDatesSelected   <a id="distributoroffereddatesselected"></a>

Alternative dates when there is no availability selected.

#### distributorCategoryGalleryOpened   <a id="distributorcategorygalleryopened"></a>

Category gallery was opened.

#### distributorRoomSelected   <a id="distributorroomselected"></a>

A room \(or other space type\) was selected.

| Data Layer Variable Name | Description |
| :--- | :--- |
| roomId | Unique identifier of the selected room. |
| roomName | Name of the selected room in the hotel’s default language. |
| spaceType | Name of the selected room’s space type, one of`Room`,`Bed`or`Dorm`. |

#### distributorSpaceTypeCountChanged   <a id="distributorspacetypecountchanged"></a>

A number of the selected “rooms” in the order was changed.

| Data Layer Variable Name | Description |
| :--- | :--- |
| count | Number of the selected space types. |

#### distributorRoomOccupancyChanged   <a id="distributorroomoccupancychanged"></a>

An occupation \(adults and children counts\) was changed for the one room \(or similar\) space type.

| Data Layer Variable Name | Description |
| :--- | :--- |
| roomIndex | Index of the changed room. |
| adultCount | Number of the selected adults. |
| childCount | Number of the selected children. |

#### distributorProductAdded   <a id="distributorproductadded"></a>

A product was added to the order.

| Data Layer Variable Name | Description |
| :--- | :--- |
| productId | Unique identifier of the added product. |
| productName | Name of the product in the hotel’s default language. |

#### distributorProductRemoved   <a id="distributorproductremoved"></a>

A product was removed from the order.

| Data Layer Variable Name | Description |
| :--- | :--- |
| productId | Unique identifier of the removed product. |
| productName | Name of product in the hotel’s default language. |

#### distributorRoomAdded   <a id="distributorroomadded"></a>

A room/multiple rooms were added to the order.

| Data Layer Variable Name | Description |
| :--- | :--- |
| reservations.orderId | Unique identifier used only within session to identify order items |
| reservations.hotelId | Unique identifier of selected hotel |
| reservations.roomId | Unique identifier of selected room |
| reservations.rateId | Unique identifier of selected rate |
| reservations.productIds | Collection of selected product unique identifiers |
| reservations.startDate | Reservation start date |
| reservations.endDate | Reservation end date |
| reservations.adultCount | Number of selected adults |
| reservations.childCount | Number of selected children |

#### distributorRoomCountChanged   <a id="distributorroomcountchanged"></a>

The quantity of rooms in the order was increased or decreased

| Data Layer Variable Name | Description |
| :--- | :--- |
| orderId | Unique ID used only within session to identify order items |
| roomId | Unique identifier of selected room |
| rateId | Unique identifier of selected rate |
| countChange | Change of quantity \(e.g. 1, -1\) |

#### distributorBookingPrepared   <a id="distributorbookingprepared"></a>

A booking is prepared and user needs to enter their details. This event triggers when user reaches Checkout step.

| Data Layer Variable Name | Description |
| :--- | :--- |
| totalCost | current total cost of the reservation group, in the hotel’s default currency |

#### distributorBookingFinished   <a id="distributorbookingfinished"></a>

A booking was made. This event triggers once every reservation group is made.

| Data Layer Variable Name | Description |
| :--- | :--- |
| reservationGroupId | id of the reservation group |
| totalCost | total cost of the reservation group, in the hotel’s default currency |
| currencyCode | hotel’s default currency code in ISO format |

#### distributorReservationCreated   <a id="distributorreservationcreated"></a>

A reservation was created. This event triggers when each reservation is made in the reservation group.

| Data Layer Variable Name | Description |
| :--- | :--- |
| customerEmail | the customer’s email |
| customerName | the customer’s name |
| currencyCode | hotel’s default currency code in ISO format |
| reservationGroupId | id of the reservation group |
| id | id of the reservation |
| roomId | id of the room category |
| rateId | id of the rate of the reservation |
| number | confirmation number of the reservation |
| roomName | name of the room |
| startDate | start date of the reservation |
| endDate | end date of the reservation |
| nights | total nights spent |
| cost | cost of the reservation in the hotel’s default currency |
| alternativeCost | cost of the reservation in all currencies supported by the property as \(key: currency, value: price\) dictionary/object. |
