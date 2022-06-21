# Availability blocks

## Get Availability blocks

Get availability block details for specified booking engine instance, that modifies your availability of space categories, and rates.
This operation can be called initially to fetch data which may be important during the booking workflow.
Availability block can restrict your booking engine's calendar to specific interval defined by `StartUtc` and `EndUtc` in the response, it also gives you `RateId` that should be used.

### Request

`[ApiBaseUrl]/api/distributor/v1/availabilityBlocks/getAll`

```json
{
    "Client": "My Client 1.0.0",
    "AvailabilityBlockIds": [
        "5mgbe1b4-6739-40b7-81b3-d369d9469c48"
    ],
    "EnterpriseId": "3edbe1b4-6739-40b7-81b3-d369d9469c48"
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Client` | string | required | Identification of the API client, as described in [Authorization](../guidelines/authorization.md). |
| `EnterpriseId` | string | required | Unique identifier of the hotel (enterprise). |
| `AvailabilityBlockIds` | array of string | required | Set of unique identifier of availabilityBlockId usually provided in query parameter on private link to your booking engine. |

### Response

```json
{
    "AvailabilityBlocks":[
      {
        "Id": "5mgbe1b4-6739-40b7-81b3-d369d9469c48",
        "Name": "Name of the availability block",
        "ServiceId": "a64f85bf-b92c-4df7-b7c8-ab7c00adc59a",
        "RateId": "038a88e6-17c6-4553-b036-aebb00a9bc4c",
        "StartUtc": "2022-06-27T22:00:00Z",
        "EndUtc": "2022-07-04T22:00:00Z"
      }
    ]
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Id` | string | required | Provided ID of availability block. |
| `Name` | string | required | Name of availability block. |
| `ServiceId` | string | required | Unique identifier of [Service](configuration.md#service) to which availability block is assigned |
| `RateId` | string | required | Unique identifier of [Rate](hotels.md#rate) which is intended for this availability block |
| `StartUtc` | string | required | Availability block start date \(validity start date\) in ISO 8601 format. |
| `EndUtc` | string | required | Availability block end date \(validity expiration date\) in ISO 8601 format. |

## How to obtain availabilityBlockId
In Mews Operations you generate availability block in desired property. From the user interface you get `availabilityBlockId` that can be used with some of yours booking engine configurations.

## How to work with availability blocks
- In your application, after you receive details about your availability block via [Get Availability blocks](availability-blocks.md#get-availability-blocks) you need to check if current date is between `StartUtc` and `EndUtc` interval. Otherwise, you can display, that availability block already expired.
- Then in your custom Booking Engine, you must provide `availabilityBlockId` into all endpoints, that accepts it.
- Filter [Rates](hotels.md#rate) with received availability block `rateId`. Only this Rate should available and bookable for this booking engine session.

### Endpoints accepting `availabilityBlockId`:
- [Get availability](hotels.md#get-availability)
- [Get reservations pricing](reservations.md#get-reservations-pricing)
- [Create reservation group](reservation-groups.md#create-reservation-group)
