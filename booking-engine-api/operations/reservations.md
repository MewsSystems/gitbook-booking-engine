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
