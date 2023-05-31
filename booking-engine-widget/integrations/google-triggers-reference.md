# Google Triggers Reference

> **Notice of usage:** Google Tag Manager is a third party service and we provide this integration as is. We export a set of supported events and their data to the container, however, we have no control over what happens to them and how they are used. Below we provide a set of basic setup examples that have been tested and verified to work with the Mews Booking Engine. If you need a more complex setup, it is up to you to configure and test it.

All events data is passed to Tag Manager through _Data Layer_. To use it in your tags, set up _Variable_ with a proper name as a variable of the data layer, like this:

![variable](../../.gitbook/assets/variable.png)

> **Note:** All prices currently presented via the data layer are gross \(including taxes and fees\).

## Google Analytics 4 (GA4 events)

List of all available events:

**Step / pageview events**

* ga4_ApplicationLoaded
* ga4_VoucherAdded
* ga4_PropertiesLoaded
* ga4_CalendarLoaded
* ga4_CategoriesLoaded
* ga4_RatesLoaded
* ga4_ProductsLoaded
* ga4_PromotedServicesLoaded
* ga4_SummaryLoaded
* ga4_DetailsLoaded
* ga4_BookingCreated
* ga4_ConfirmationLoaded

**Extra events**

* ga4_FetchedWithOccupancy

**GA4 eCommerce events**

* select_promotion
* view_item_list
* add_to_cart
* remove_from_cart
* begin_checkout
* add_payment_info
* purchase

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
| enterpriseName | Array with languages translated names of enterprise |

Pageload events with 'ga4_' prefix have as well following attributes available in datalayer:

| Data Layer Variable Name | Description |
| :-- | :-- |
| page_location | URL style location to be used for tracking URL |
| page_title | Human readable name of screen|

Some events expose additional data layer variables. They are described separately for each event.

### TrackingConsents

| Name | Type | Contract | Purpose |
| :-- | :-- | :-- | :-- |
| advertising | boolean | required | Advertising, e.g. used to help advertisers deliver more relevant advertising, or to limit how many times you see an advertisment. |
| functional | boolean | required | Unnecessary functionality, e.g. remembering user choices made in the past. |
| necessary | boolean | required | Necessary functionality. |
| performance | boolean | required | Performance, e.g. collecting information about how users use a website; data are anonymized. |


### Step / pageview events

#### ga4_ApplicationLoaded

Event which fires when the application is loaded for user

#### ga4_VoucherAdded

Voucher have been added into booking

| Data Layer Variable Name | Description |
| :-- | :-- |
| voucherCode | Code of voucher added by user |

#### ga4_PropertiesLoaded

Step of properties selection was loaded for user

#### ga4_CalendarLoaded

Calendar step have been loaded for user

#### ga4_CategoriesLoaded

Categories / Room selection have been shown to user

| Data Layer Variable Name | Description |
| :-- | :-- |
| startDate | Start of stay date selected by user |
| endDate | End of stay date selected by user |
| available | Array of room categories which have been shown to user as available |
| unavailable | Array of room categories which have been shown to user as not available |

Each of the items in arrays follows the google [Item specification for ecommerce](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce?client_type=gtag)

Example

```
{
      item_id: "0d9120fc-72cb-4d23-afe2-ad9000dcb803",
      item_name: "Room 1",
      item_category2: "Jan's Hotel",
      item_category3: "Jan's Hotel City",
      item_brand: "Jan's Hotel Chain",
      affiliation: "Jan's Hotel",
      enterpriseId: "6aaf20ac-a651-4826-b8c0-ad9000dcac3d",
      currency: "EUR",
      price: 10
    },
```

#### ga4_RatesLoaded

Rates selection have been shown to user

| Data Layer Variable Name | Description |
| :-- | :-- |
| rates | Array of rates shown to user, together with their currency and gross price. |

#### ga4_ProductsLoaded

Products selection have been shown to user

| Data Layer Variable Name | Description |
| :-- | :-- |
| products | Array of products shown to user |

#### ga4_PromotedServicesLoaded

Promoted Services have been shown to user

#### ga4_SummaryLoaded

Summary step have been shown to user

#### ga4_DetailsLoaded

Final screen with form to fill have been shown to user

#### ga4_BookingCreated

Mews created booking within the PMS. Additional information are available in `purchase` event

#### ga4_ConfirmationLoaded

Confirmation screen have been shown to user, this step is shown after returning from Payment gateway as final step of the process

### Extra events

#### ga4_FetchedWithOccupancy

Dates screen has been submitted with selected occupancy in the form.

| Data Layer Variable Name | Description                                                                              |
|:-------------------------|:-----------------------------------------------------------------------------------------|
| adultCount               | Number - total count of `Adult` ageCategories selected in the Dates step occupancy form. |
| childCount               | Number - total count of `Child` ageCategories selected in the Dates step occupancy form. |


### GA4 eCommerce events

Please follow the google guide for tracking eCommerce in GA4. YOu need to set up events with all mandatory parameters so they are tracked correctly.
We are pushing all available variables into the eCommerce tracking for more advanced setups as well.
All mandatory and supported fields
> [Google eCommerce support page](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce)

#### select_promotion

Voucher have been added to reservation

| Data Layer Variable Name | Description |
| :-- | :-- |
| promotion_id | Array of rates shown to user |

#### view_item_list

List of available rooms show to user for eCommerce purpose

| Data Layer Variable Name | Description |
| :-- | :-- |
| items | Array of items (rooms / categories) shown to user |

#### add_to_cart

User added room and products to cart

| Data Layer Variable Name | Description |
| :-- | :-- |
| items | Array of items (rooms / categories / products) added by user in reservation |

Example:

```
{
  event: "add_to_cart",
  items: [
    {
      item_id: "0d9120fc-72cb-4d23-afe2-ad9000dcb803",
      quantity: 1,
      item_name: "Room 1",
      item_variant: "Best Price",
      item_category: "Reservation",
      item_category2: "Jan's Hotel",
      item_category3: "Jan's Hotel City",
      item_brand: "Jan's Hotel Chain",
      affiliation: "Jan's Hotel",
      currency: "EUR",
      price: 42
    },
    {
      item_id: "26c2ec6e-2890-4677-b994-ad9000dce77f",
      quantity: 1,
      item_name: "Dog",
      item_category: "Product",
      item_category2: "Jan's Hotel",
      item_category3: "Jan's Hotel City",
      item_brand: "Jan's Hotel Chain",
      affiliation: "Jan's Hotel"
    }
  ],
  trackingConsents: {
    necessary: true,
    performance: true,
    functional: true,
    advertising: true
  },
  gtm: {uniqueEventId: 54}
}
```

#### remove_from_cart

In case user removed item from cart, this event is triggered. See `add_to_cart` event parameters

| Data Layer Variable Name | Description |
| :-- | :-- |
| items | Array of items (rooms / categories / products) remover by user in reservation |

#### begin_checkout

User started the process of checkout. See `add_to_cart` event parameters

| Data Layer Variable Name | Description |
| :-- | :-- |
| items | Array of items (rooms / categories / products) added by user in reservation |

#### add_payment_info

User added the payment information

| Data Layer Variable Name | Description |
| :-- | :-- |
| payment_type | Payment type, usually `PaymentCard` |
| currency | Currency in which the payment will be done |
| value | Amount of the reservation |
| items | Array of items (rooms / categories / products) added by user in reservation |

#### purchase

Most important eCommerce event.
We are exposing many variables in the event which can be used for advanced tracking. See the example for full description.
Most important variables

| Data Layer Variable Name | Description |
| :-- | :-- |
| startDate | Start of stay date selected by user |
| endDate | End of stay date selected by user |
| currency | Currency in which the payment will be done |
| value | Amount of the reservation |
| tax | Amount of tax for the reservation |
| reservationGroupName | ID / Name of the reservation group created in Mews |
| netValue | Value of reservation without taxes |
| grossValue | Value of reservation with all taxes |
| pricingMode | either `gross` for US style of pricing, `net` for EU style of pricing |
| roomCount | Count of rooms in reservation |
| adults | Count of Adults in reservations |
| children | Count of children in reservations |
| items | Array of items (rooms / categories / products) added by user in reservation. See example for different types of items |

Example:
```
{
  event: "purchase",
  gtm: {uniqueEventId: 18, start: 1661784899375},
  eventName: "Confirmation Loaded", 
  id: "6aaf20ac-a651-4826-b8c0-ad9000dcac3d",
  name: "Jan's Hotel", 
  languageCode: "en-GB", 
  hotelName: "Jan's Hotel", // Property name
  hotelId: "6aaf20ac-a651-4826-b8c0-ad9000dcac3d",
  page_location: "/confirmation",
  page_title: "Confirmation",
  items: [ // Rooms added to reservation group. There can be multiple items with different dates and confirmation numbers. Ideally, you map all, you can as well map just one as 95% of reservations will have only one item.
    {
      item_id: "244e472a-4e47-4445-8677-af0000f58111", // Room category id
      item_name: "Room 1", // Room category name
      item_variant: "Best Price", // Selected rate
      item_category: "Reservation",
      item_category2: "Jan's Hotel", // Property name
      item_category3: "Jan's Hotel City", // Property city
      item_brand: "Jan's Hotel Chain", // Property chain
      affiliation: "Jan's Hotel",
      currency: "EUR",
      price: 20, // Price of reservation
      netPrice: 18.7, // Price of reservation without taxes
      grossPrice: 20,  // Price of reservation with taxes
      pricingMode: "Gross", // Pricing mode (Gross mainly Europe = tax is included in price, Net mainly US = tax non included in price)
      quantity: 1, // Count of rooms of room category
      reservationGroupId: "2cf7e37b-b1d1-4970-8aaf-af0000f580f2",
      reservationGroupName: "Name-29-8-8617", // Reservation Group name – can be mapped to export from mews Operations for each reservation
      confirmationNumber: "194", // Confirmation number of each reservation to be mapped with Mews operations
      reservationRateName: "Best Price",
      checkInDate: "2022-08-29", // Check-in day of reservation
      checkOutDate: "2022-08-31", // Check-out day of reservation
      tax: 1.3, // Tax of reservation
      stayDuration: 2,  // Count of days in reservation
      adults: 2, // Count of adults in  reservation
      children: 0 // Count of children in reservation
    }
  ],
  affiliation: "Jan's Hotel",
  transaction_id: "2cf7e37b-b1d1-4970-8aaf-af0000f580f2", // Changed to Reservation Group ID – will be added to export in Mews Operation to identify each reservation group
  currency: "EUR",
  value: 20, // Total price of reservation group
  tax: 1.3, // Total tax of reservation group
  reservationGroupId: "2cf7e37b-b1d1-4970-8aaf-af0000f580f2", // Reservation Group ID – will be added to export in Mews Operation to identify each reservation group
  reservationGroupName: "Name-29-8-8617", // Reservation Group name – can be mapped to export from mews Operations for each reservation
  reservationIds: "244e472a-4e47-4445-8677-af0000f58111", // Comma separated list of all reservation (item) IDs
  chainName: "Jan's Hotel Chain", // Chain name
  netValue: 18.7, // Price without taxes
  grossValue: 20, // Price with taxes
  pricingMode: "Gross", // Pricing mode (Gross mainly Europe = tax is included in price, Net mainly US = tax non included in price)
  roomCount: 1, // Count of rooms
  adults: 2, // Count of adults
  children: 0 // Count of children
}
```

## Deprecated - Universal Analytics events - will

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
| currencyCode | Currency code in ISO format, i.e`EUR`. [Supported currency codes](../../booking-engine-api/guidelines/supported-currency-codes.md) |
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
