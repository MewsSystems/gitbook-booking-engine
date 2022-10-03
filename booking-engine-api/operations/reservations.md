# Reservations

## Get reservations pricing

Get a price quotation for a specific hotel, date interval, room category and person count.

### Request

`[ApiBaseUrl]/api/distributor/v1/reservations/getPricing`

```json
{
    "Client": "My Client 1.0.0",
    "HotelId": "3edbe1b4-6739-40b7-81b3-d369d9469c48",
    "StartUtc": "2015-01-01T00:00:00Z",
    "EndUtc": "2015-01-03T00:00:00Z",
    "VoucherCode": "Discount2042",
    "RoomCategoryId": "3540c7d4-e128-41e2-81d8-ff4d196c595a",
    "Occupancies": [
        {
            "AdultCount": 2,
            "ChildCount": 0
        }
    ],
    "ProductIds": [
        "d0e88da5-ae64-411c-b773-60ed68954f64"
    ],
    "AvailabilityBlockId": "5mgbe1b4-6739-40b7-81b3-d369d9469c48"
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Client` | string | required | Identification of the client as described in [Authorization](../guidelines/authorization.md). |
| `HotelId` | string | required | Unique identifier of the hotel. |
| `StartUtc` | string | required | Start date of the reservation, i.e. arrival date. |
| `EndUtc` | string | required | End date of the reservation, i.e. departure date. |
| `VoucherCode` | string | optional | Voucher code enabling special rate offerings. |
| `RoomCategoryId` | string | required | Identifier of the requested room category. |
| `Occupancies` | array of [Occupancy](#occupancy) | required | Occupancy numbers for the reservations. |
| `ProductIds` | array of string | optional | Unique identifiers of the requested products. |
| `AvailabilityBlockId` | string | optional | Unique identifier of availability block if present. Provide always when you have it.  |

#### Occupancy

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `AdultCount` | number | required | Number of adults. |
| `ChildCount` | number | required | Number of children. |

### Response

```json
{
    "OccupancyPrices": [
        {
            "AdultCount": 1,
            "ChildCount": 0,
            "Pricing": [
                {
                    "MaxPrice": {
                        "TotalAmount": { },
                        "AverageAmountPerTimeUnit": { }
                    },
                    "Price": {
                        "TotalAmount": { },
                        "AverageAmountPerTimeUnit": { }
                    },
                    "RateId": "b34330be-7e19-453e-8959-592c4e820f85"
                }
            ]
        }
    ]
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `OccupancyPrices` | array of [Room occupancy availability](hotels.md#room-occupancy-availability) | required | Pricing information. |



## Get reservation price

Get a final price of requested reservation

### Request

`[ApiBaseUrl]/api/distributor/v1/reservations/price`

```json
{
    "Client": "My Client 1.0.0",
    "ConfigurationId": "5dfgaeb5-5848-81b3-40b7-d102e96kcf52",
    "CurrencyCode": "EUR",
    "Reservations": [
      {
        "Identifier": "uniqueClientGeneratedIdentifier1",
        "StartUtc": "2015-01-01T00:00:00Z",
        "EndUtc": "2015-01-03T00:00:00Z",
        "ProductIds": [],
        "VoucherCode": null,
        "RateId": "c1d48c54-9382-4ceb-a820-772bf370573d",
        "RoomCategoryId": "4037c0ec-a59d-43f1-9d97-d6c984764e8c",
        "AdultCount": 2,
        "ChildCount": 0
      }
    ]
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Client` | string | required | Identification of the client as described in [Authorization](../guidelines/authorization.md). |
| `ConfigurationId` | string | required | Unique identifier of the Booking Engine configuration used. |
| `CurrencyCode` | string | optional | ISO 4217 code of the currency in which price will be calculated in. Enterprise default currency code is used as default. [Supported currency codes](../guidelines/supported-currency-codes.md)|
| `Reservations` | array of [Reservation](#reservation) | required | Unique identifier of the Booking Engine configuration used. |

#### Reservation

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `AdultCount` | number | required | Number of adults. |
| `ChildCount` | number | required | Number of children. |
| `Identifier` | string | required | Unique identifier for reservation generated on client. |
| `StartUtc` | string | required | Start date of the reservation, i.e. arrival date. |
| `EndUtc` | string | required | End date of the reservation, i.e. departure date. |
| `ProductIds` | array of string | optional | Unique identifiers of products which should be included into reservation price calculations. |
| `VoucherCode` | string | optional | Voucher code applied to reservation |
| `RateId` | string | required | Identifier of the chosen rate. |
| `RoomCategoryId` | string | required | Unique identifier of the room category. |


### Response

```json
{
  "ReservationPrice": [
    {
      "Identifier": "uniqueClientGeneratedIdentifier1",
      "TotalAmount": {
        "Currency": "EUR",
        "GrossValue": 203.00,
        "NetValue": 184.82,
        "TaxValues": [
          {
            "TaxRateCode": "ES-2016-R",
            "Value": 18.18
          }
        ],
        "Breakdown": {
          "Items": [
            {
              "TaxRateCode": "ES-2016-R",
              "NetValue": 181.82,
              "TaxValue": 18.18
            },
            {
              "TaxRateCode": null,
              "NetValue": 3.0,
              "TaxValue": 0.0
            }
          ]
        }
      },
      "AmountToChargeOnConfirmation": null,
      "ProductOrderPrices": [
        {
          "ProductId": "47c186ec-7b2b-43f2-95fb-abc800c82505",
          "AgeCategoryId": null,
          "ProductName": {
            "es-ES": "Bicicleta",
            "en-US": "Bike Rental"
          },
          "ProductOptions": {
            "SelectedByDefault": false,
            "BillAsPackage": false,
            "OfferToCustomer": true,
            "ExcludePriceFromOffer": false,
            "OfferToEmployee": true
          },
          "ChargingMode": "Once",
          "TotalAmount": {
            "Currency": "EUR",
            "GrossValue": 3.0,
            "NetValue": 3.0,
            "TaxValues": [],
            "Breakdown": {
              "Items": [
                {
                  "TaxRateCode": null,
                  "NetValue": 3.0,
                  "TaxValue": 0.0
                }
              ]
            }
          }
        }
      ]
    }
  ]
}
```

#### ReservationPrice

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Identifier` | string | required | Unique identifier for reservation provided in the request data |
| `AmountToChargeOnConfirmation` | [Amount](#totalamount) | optional | Amount that needs to be charged on payment gateway on reservationGroup confirmation |
| `TotalAmount` | [Total Amount](#totalamount) | required | `TotalAmount` object of the reservation |
| `ProductOrderPrices` | array of [ProductOrderPrice](#productorderprice) | required | List of `ProductOrderPrice` objects assigned to reservation |

#### ProductOrderPrice
| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `ProductId` | string | required | Unique identifier of product |
| `AgeCategoryId` | string | optional | Identifier of age category. |
| `ProductName` | [Localized text](hotels.md#localized-text) | required | Name of the hotel. |
| `ProductOptions` | [ProductOptions](#productoptions) | required | Product options |
| `ChargingMode` | string [Product charging mode](hotels.md#product-charging-mode) | required | Charging mode of the product. |
| `TotalAmount` | [Total Amount](#totalamount) | required | Total amount of product. |

##### ProductOptions
| Property | Type | Contract | Description |
| :-- | :-- | :-- |
| `SelectedByDefault` | boolean  | If product was selected by default for reservation  |
| `BillAsPackage` | boolean  | Product is part of a package |
| `OfferToCustomer` | boolean  | Product is available in booking engine |
| `ExcludePriceFromOffer` | boolean  | Product was not available in booking engine, but it is counted in reservation total price ( eg. CityTax ) |
| `OfferToEmployee` | boolean  | Product available in mews operations |

##### TotalAmount
Is composed of [Amount](reservation-groups.md#amount) extended of `Breakdown` with `Items` of array of [Tax value](#tax-value)

##### Tax value
| Property | Type | Description |
| :-- | :-- | :-- |
| `TaxRateCode` | string | Unique identifier of Tax Rate Code. |
| `NetValue` | Number | Net amount of product |
| `TaxValue` | Number | Tax amount of product ( Calculated from NetValue based on TaxRateCode ) |
