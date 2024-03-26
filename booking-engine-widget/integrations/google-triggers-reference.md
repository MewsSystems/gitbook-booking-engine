# Google Triggers Reference

> **Notice of usage:** Google Tag Manager (GTM) and Google Analytics 4 (GA4) are third party services and we provide this integration as is.
We support a set of custom events and Data Layer variables for use with GTM and GA4, however we have no control over what happens to them and how they are used. The basic setup examples we provide have been tested and verified to work with the Mews Booking Engine, however if you need a more complex setup then we cannot provide the support to do so and we recommend to ask a specialist to set it up and test it for you.

This reference provides details of **custom events** and **Data Layer variables** generated within the Booking Engine, which can be used to trigger analytics tags to fire, i.e. to send data to Google Analytics.
You will need to reference these events and variables when setting up tag _triggers_ in Google Tag Manager.

## Contents

* [Data Layer variables](#data-layer-variables)
* [Custom events](#custom-events)
* [GA4 pageview events](#ga4-pageview-events)
* [GA4 eCommerce events](#ga4-ecommerce-events)

## Data Layer variables

All event data is passed to Google Tag Manager through a _Data Layer_.

> ### What is a Data Layer?
> A Data Layer is a Javascript object in a website or app that collects analytics data in a standardized way. It acts as a layer between the site and the tag management system.
> The layer stores values, such as page name and URL, that are populated automatically when a visitor uses the site.
> The data is transferred into tag management variables and can be used to activate triggers in your tag configurations.
> [Google Help — The data layer](https://support.google.com/tagmanager/answer/6164391?hl=en)

To use data from the Data Layer in your tags, in the GTM configuration set up a _Variable_ with a suitable name as a Data Layer Variable (DLV), like this:

![variable](../../.gitbook/assets/variable.png)

The [Custom events](#custom-events) reference below describes which Data Layer Variables are relevant to which custom events.

> **Prices:** Note all prices currently presented via the Data Layer are gross prices, i.e. including taxes and fees.

## Custom events

**GA4 pageview events**

* [ga4_ApplicationLoaded](#ga4_applicationloaded)
* [ga4_VoucherAdded](#ga4_voucheradded)
* [ga4_PropertiesLoaded](#ga4_propertiesloaded)
* [ga4_CalendarLoaded](#ga4_calendarloaded)
* [ga4_CategoriesLoaded](#ga4_categoriesloaded)
* [ga4_RatesLoaded](#ga4_ratesloaded)
* [ga4_ProductsLoaded](#ga4_productsloaded)
* [ga4_PromotedServicesLoaded](#ga4_promotedservicesloaded)
* [ga4_SummaryLoaded](#ga4_summaryloaded)
* [ga4_DetailsLoaded](#ga4_detailsloaded)
* [ga4_BookingCreated](#ga4_bookingcreated)
* [ga4_ConfirmationLoaded](#ga4_confirmationloaded)

**GA4 eCommerce events**

* [select_promotion](#select_promotion)
* [view_item_list](#view_item_list)
* [add_to_cart](#add_to_cart)
* [remove_from_cart](#remove_from_cart)
* [begin_checkout](#begin_checkout)
* [add_payment_info](#add_payment_info)
* [purchase](#purchase)

### Data Layer Variables in events

Each event is fired with a standard set of data:

| Data Layer Variable Name | Description |
| :-- | :-- |
| eventName | Name of the event, in readable form without prefix, e.g. `Voucher Added`. |
| trackingConsents | [Tracking consents](#tracking-consents) applied at the time the event was created. |

If a user selects a hotel or property in the Booking Engine, information about it is also added to the event. In _Singlehotel_ mode, the property is always selected.

| Data Layer Variable Name | Description |
| :-- | :-- |
| hotelName | Name of the hotel or property |
| hotelId | Unique identifier of the hotel or property |
| enterpriseName | Array with name of the enterprise (hotel / property) in each supported language |

Pageload events with the 'ga4_' prefix also have the following attributes available in the Data Layer:

| Data Layer Variable Name | Description |
| :-- | :-- |
| page_location | URL style location, to be used for tracking URL |
| page_title | Human readable name of page or screen|

Some events expose additional DLVs. These are described separately for each event.

### Tracking consents

| Name | Type | Contract | Purpose |
| :-- | :-- | :-- | :-- |
| advertising | boolean | required | Advertising, e.g. used to help advertisers deliver more relevant advertising, or to limit how many times you see an advertisment. |
| functional | boolean | required | Functional, non-essential functionality, e.g. remembering user choices made in the past. |
| necessary | boolean | required | Necessary functionality. |
| performance | boolean | required | Performance, e.g. collecting information about how users use a website; data are anonymized. |

## GA4 pageview events

### ga4_ApplicationLoaded

* Event which fires when the application is loaded for the user

### ga4_VoucherAdded

* A voucher has been added into the booking

| Data Layer Variable Name | Description |
| :-- | :-- |
| voucherCode | Code of voucher added by user |

### ga4_PropertiesLoaded

* The properties selection step was loaded for the user

### ga4_CalendarLoaded

* The calendar step has been loaded for the user

### ga4_CategoriesLoaded

* Categories / room selection has been shown to the user

| Data Layer Variable Name | Description |
| :-- | :-- |
| startDate | Start of stay date selected by user |
| endDate | End of stay date selected by user |
| available | Array of room categories which have been shown to user as available |
| unavailable | Array of room categories which have been shown to user as not available |

* Each of the items in arrays follows the google [Item specification for ecommerce](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce?client_type=gtag), for example:

```javascript
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

### ga4_RatesLoaded

* Rates selection has been shown to the user

| Data Layer Variable Name | Description |
| :-- | :-- |
| rates | Array of rates shown to user, together with their currency and gross price |

### ga4_ProductsLoaded

* Products selection has been shown to the user

| Data Layer Variable Name | Description |
| :-- | :-- |
| products | Array of products shown to user |

### ga4_PromotedServicesLoaded

* Promoted Services has been shown to the user

### ga4_SummaryLoaded

* Summary step has been shown to the user

### ga4_DetailsLoaded

* The final screen with form to fill in has been shown to the user

### ga4_BookingCreated

* Mews created a booking within the PMS. Additional information is available in the `purchase` event.

### ga4_ConfirmationLoaded

* The confirmation screen has been shown to the user. This step is shown after returning from the payment gateway as the final step of the process.

## GA4 eCommerce events

Please follow the [Google guide for tracking eCommerce in GA4](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce). You need to set up events with all mandatory parameters so they are tracked correctly.
We are pushing all available variables into the eCommerce tracking for more advanced setups as well.

### select_promotion

* Voucher has been added to the booking

| Data Layer Variable Name | Description |
| :-- | :-- |
| promotion_id | Array of rates shown to user |

### view_item_list

* List of available rooms shown to user for eCommerce purposes

| Data Layer Variable Name | Description |
| :-- | :-- |
| items | Array of items (rooms / categories) shown to user |

### add_to_cart

* User added room and products to cart

| Data Layer Variable Name | Description |
| :-- | :-- |
| items | Array of items (rooms / categories / products) added by user in reservation |

* Example:

```javascript
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

### remove_from_cart

* User removed an item from the cart. See `add_to_cart` for event parameters.

| Data Layer Variable Name | Description |
| :-- | :-- |
| items | Array of items (rooms / categories / products) remover by user in reservation |

### begin_checkout

* User started the process of check-out. See `add_to_cart` for event parameters.

| Data Layer Variable Name | Description |
| :-- | :-- |
| items | Array of items (rooms / categories / products) added by user in reservation |

### add_payment_info

* User added payment information.

| Data Layer Variable Name | Description |
| :-- | :-- |
| payment_type | Payment type, usually `PaymentCard` |
| currency | Currency in which the payment will be done |
| value | Amount of the reservation |
| items | Array of items (rooms / categories / products) added by user in reservation |

### purchase

* Purchase made. This is the most important eCommerce event. We expose many variables in the event which can be used for advanced tracking. See the example for full description.
* The most important variables are:

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

* Example:

```javascript
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
