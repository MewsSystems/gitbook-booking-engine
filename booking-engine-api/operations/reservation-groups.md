# Reservation groups

## Create reservation group

### Request

`[ApiBaseUrl]/api/distributor/v1/reservationGroups/create`

```json
{
    "Client": "My Client 1.0.0",
    "ConfigurationId": "5dfgaeb5-5848-81b3-40b7-d102e96kcf52",
    "HotelId": "3edbe1b4-6739-40b7-81b3-d369d9469c48",
    "Customer": {
        "Email": "hiro@snow.com",
        "FirstName": "Hiro",
        "LastName": "Protagonist",
        "Telephone": "",
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "PostalCode": "",
        "StateCode": "",
        "NationalityCode": "",
        "SendMarketingEmails": false
    },
    "Booker": {
        "Email": "john.doe@snow.com",
        "FirstName": "John",
        "LastName": "Doe",
        "Telephone": "654257001458",
        "SendMarketingEmails": true
    },
    "Reservations": [
        {
            "RoomCategoryId": "4037c0ec-a59d-43f1-9d97-d6c984764e8c",
            "StartUtc": "2015-01-01T00:00:00Z",
            "EndUtc": "2015-01-03T00:00:00Z",
            "VoucherCode": "Discount2042",
            "RateId": "c1d48c54-9382-4ceb-a820-772bf370573d",
            "AdultCount": 3,
            "ChildCount": 0,
            "ProductIds": [
                "d0e88da5-ae64-411c-b773-60ed68954f64"
            ],
            "Notes": "Quiet room please."
        }
    ],
    "CreditCardData": {
        "PaymentGatewayData": "...",
        "Expiration": "2030-10",
        "HolderName": "John Smith"
    }
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Client` | string | required | Identification of the client as described in [authorization](./authorization.md). |
| `ConfigurationId` | string | required | Unique identifier of the used Distributor configuration. |
| `HotelId` | string | required | Unique identifier of the hotel. |
| `Customer` | [Customer](./operations.md#customer) | required | Information about customer who creates the order. |
| `Booker` | [Booker](./operations.md#booker) | optional | Information about booker. |
| `Reservations` | array of [Reservation data](./operations.md#reservation-data) | required | Parameters of reservations to be ordered. |
| `CreditCardData` | [Credit card data](./operations.md#credit-card-data) | optional | Credit card data, required if hotel has payment gateway. |

#### Customer

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Email` | string | required | Email of the customer. |
| `FirstName` | string | required | First name of the customer. |
| `LastName` | string | required | Last name of the customer. |
| `Telephone` | string | optional | Telephone number of the customer. |
| `AddressLine1` | string | optional | First line of the address. |
| `AddressLine2` | string | optional | Second line of the address. |
| `City` | string | optional | City. |
| `PostalCode` | string | optional | Postal code of the address. |
| `StateCode` | string | optional | ISO 3166-2 code of the state, e.g.`US-AL`. |
| `NationalityCode` | string | optional | ISO 3166-1 Aplha-2 code of the customer’s nation country, e.g.`US`. |
| `SendMarketingEmails` | boolean | optional | Subscribe to marketing emails. When booker is present, this should be `false` or `null` because customer is not subscribing - the Booker is. |

#### Booker

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Email` | string | required | Email of the booker. |
| `FirstName` | string | required | First name of the booker. |
| `LastName` | string | required | Last name of the booker. |
| `Telephone` | string | optional | Telephone number of the booker. |
| `SendMarketingEmails` | boolean | optional | Subscribe to marketing emails. When booking on behalf of somebody else, this field should have the value and the field `SendMarketingEmails` in [customer](./operations.md#customer) should either not have one, be set to `false` or `null`. API accepts following values: `true` - the subscription is created, `false` - subscription is disabled, not supplied or `null` - subscription remains untouched. |

#### Reservation data

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `RoomCategoryId` | string | required | Identifier of the requested room category. |
| `StartUtc` | string | required | Start date of the reservation \(arrival date\). |
| `EndUtc` | string | required | End date of the reservation \(departure date\). |
| `VoucherCode` | string | optional | A voucher code, set to be paired with reservation for later retrieval only. Actual voucher rate used is determined by setting a proper `RateId`. |
| `RateId` | string | required | Identifier of the chosen rate. |
| `AdultCount` | number | required | Number of adults. |
| `ChildCount` | number | required | Number of children. |
| `ProductIds` | array of string | optional | Unique identifiers of the requested products. |
| `Notes` | string | optional | Additional notes. |

#### Credit card data

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `PaymentGatewayData` | string | required | Encoded payment card data obtained from the payment gateway specific library. More details in our [use case](./use-cases/how-to-support-payment-cards-in-booking-engine-application.md). |
| `Expiration` | string | required | Expiration date of payment card in format `YYYY-MM`. |
| `HolderName` | string | required | Name of the card holder. |

### Response

```json
{
    "Id": "f6fa7e62-eb22-4176-bc49-e521d0524dee",
    "CustomerId": "7ac6ca0d-7c08-4ab1-8da8-9b44979d8855",
    "Reservations": [
        {
            "Id": "123456ec-a59d-43f1-9d97-d6c984764e8c",
            "RoomCategoryId": "4037c0ec-a59d-43f1-9d97-d6c984764e8c",
            "StartUtc": "2015-01-01T00:00:00Z",
            "EndUtc": "2015-01-03T00:00:00Z",
            "RateId": "c1d48c54-9382-4ceb-a820-772bf370573d",
            "Rate": {
                "Id": "c1d48c54-9382-4ceb-a820-772bf370573d",
                "Name": {
                    "en-US": "Rate"
                },
                "Description": {
                    "en-US": "Best rate available."
                }
            },
            "AdultCount": 3,
            "ChildCount": 0,
            "ProductIds": [
                "d0e88da5-ae64-411c-b773-60ed68954f64"
            ],
            "Notes": "Quiet room please.",
            "Amount": { },
            "Number": "1234"
        }
    ],
    "PaymentRequestId": "2e3a700a-7b10-4e61-8e9f-acfa00ee00df",
    "PaymentCardId": "dc2f8608-9d71-47fd-9d41-ad1a009913c6",
    "TotalAmount": { }
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Id` | string | required | Unique identifier of the created reservation group. |
| `CustomerId` | string | required | Unique identifier of customer who created reservation group. |
| `Reservations` | array of [Reservation](./operations.md#reservation) | required | The created reservations in group. |
| `PaymentRequestId` | string | optional | Unique identifier of [payment request](./operations.md#payment-request) that can be used to complete [on session payment](./use-cases/on-session-payments.md). |
| `PaymentCardId` | string | optional | Unique identifier of [payment card](./operations.md#payment-card) that can be used to complete [on session payment card authorization](./use-cases/on-session-payment-card-authorization.md). |
| `TotalAmount` | [Amount](./operations.md#multi-currency-amount) | required | Total amount of the whole group. |

#### Reservation

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Id` | string | required | Identifier of the reservation. |
| `Number` | string | required | Confirmation number of the reservation. |
| `RoomCategoryId` | string | required | Identifier of the requested room category. |
| `StartUtc` | string | required | Start date of the reservation \(arrival date\). |
| `EndUtc` | string | required | End date of the reservation \(departure date\). |
| `AdultCount` | number | required | Number of adults. |
| `ChildCount` | number | required | Number of children. |
| `ProductIds` | array of string | optional | Unique identifiers of the requested products. |
| `RateId` | string | required | Identifier of the chosen rate. |
| `Notes` | string | optional | Additional notes. |
| `Amount` | [Amount](./operations.md#multi-currency-amount) | required | Total amount of the reservation. |

### Error response

In case of an error caused by insufficient availability \(which might have decreased since the time it was provided to the client\), the error response may contain the following fields on top the standard ones:

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `ExceedingReservationIndexes` | array of number | optional | Indexes of reservations from the request that are not available anymore. |

## Get reservation group

### Request

`[ApiBaseUrl]/api/distributor/v1/reservationGroups/get`

```json
{
    "Client": "My Client 1.0.0",
    "HotelId": "3edbe1b4-6739-40b7-81b3-d369d9469c48",
    "ReservationGroupId": "f6fa7e62-eb22-4176-bc49-e521d0524dee",
    "Extent": {
        "PaymentRequests": false,
        "Payments": false
    }
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Client` | string | required | Identification of the client as described in [authorization](./authorization.md). |
| `HotelId` | string | required | Unique identifier of the hotel. |
| `ReservationGroupId` | string | required | Unique identifier of the reservation group. |
| `Extent` | [Reservation group extent](./operations.md#reservation-group-extent) | optional | Extent of data to be returned. e.g it is possible to specify that together with the reservation group, payment request and payments will be returned. |

#### Reservation group extent

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `PaymentRequests` | boolean | optional | Whether the response should contain [payment requests](./operations.md#payment-request) related to the reservation group. |
| `Payments` | boolean | optional | Whether the response should contain [payment](./operations.md#payment) attempts related to the [payment requests](./operations.md#payment-request) for reservation group. |


### Response

```json
{
    "Id": "f6fa7e62-eb22-4176-bc49-e521d0524dee",
    "CustomerId": "7ac6ca0d-7c08-4ab1-8da8-9b44979d8855",
    "Reservations": [
        {
            "Id": "123456ec-a59d-43f1-9d97-d6c984764e8c",
            "RoomCategoryId": "4037c0ec-a59d-43f1-9d97-d6c984764e8c",
            "StartUtc": "2015-01-01T00:00:00Z",
            "EndUtc": "2015-01-03T00:00:00Z",
            "RateId": "c1d48c54-9382-4ceb-a820-772bf370573d",
            "Rate": {
                "Id": "c1d48c54-9382-4ceb-a820-772bf370573d",
                "Name": {
                    "en-US": "Rate"
                },
                "Description": {
                    "en-US": "Best rate available."
                }
            },
            "AdultCount": 3,
            "ChildCount": 0, 
            "ProductIds": [
                "d0e88da5-ae64-411c-b773-60ed68954f64"
            ],
            "Notes": "Quiet room please.",
            "Amount": { },
            "Number": "1234"
        }
    ],
    "PaymentRequestId": "2e3a700a-7b10-4e61-8e9f-acfa00ee00df",
    "TotalAmount": { },
    "PaymentRequests": [
        {
            "Id": "ace78dac-a0f3-420e-8a42-acfb00b9e1e5",
            "ReservationGroupId": "f6fa7e62-eb22-4176-bc49-e521d0524dee",
            "State": "Completed"
        }
    ],
    "Payments": [
        {
            "Id": "21639c17-edad-47f9-8348-acfb00b9f569",
            "EnterpriseId": "8a51f050-8467-4e92-84d5-abc800c810b8",
            "PaymentRequestId": "ace78dac-a0f3-420e-8a42-acfb00b9e1e5",
            "CreatedUtc": "2021-03-30T11:17:03Z",
            "State": "Charged",
            "Amount": {
                "Currency": "EUR",
                "GrossValue": 929.70,
                "NetValue": 929.70,
                "TaxValues": []
            },
            "ChargeAmount": {
              "Currency": "EUR",
              "GrossValue": 929.70,
              "NetValue": 929.70,
              "TaxValues": []
            }
        }
    ]
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Id` | string | required | Unique identifier of the created reservation group. |
| `CustomerId` | string | required | Unique identifier of customer who created reservation group. |
| `Reservations` | array of [Reservation](./operations.md#reservation) | required | The created reservations in group. |
| `PaymentRequestId` | string | optional | Unique identifier of payment request that can be used to complete [on session payment](./use-cases/on-session-payments.md). |
| `TotalAmount` | [Amount](./operations.md#multi-currency-amount) | required | Total amount of the whole group. |
| `PaymentRequests` | array of [Payment request](./operations.md#payment-request) | optional | Contains payment requests related to the reservation group. |
| `Payments` | array of [Payment](./operations.md#payment) | optional | Contains Payments related to the payment requests. |

#### Payment request

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Id` | string | required | Unique identifier of the payment request. |
| `ReservationGroupId` | string | required | Identifier of the related reservation group. |
| `State` | string [Payment request state](./operations.md#payment-request-state) | required | State of the payment request. |

#### Payment request state

- `Pending` - Non-finite state. Awaiting a next action.
- `Completed` - Finite state. Payment request that has been covered by payment.
- `Canceled` - Finite state. Payment request has been manually canceled by the creator (enterprise).
- `Expired` - Finite state. Payment request has not been completed within its expiration time.

#### Payment

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Id` | string | required | Unique identifier of the payment. |
| `Amount` | [Amount](./operations.md#amount) | required | Amount in a currency which was used to create [payment request](./operations.md#payment-request) - usually default currency of the enterprise. |
| `ChargeAmount` | [Amount](./operations.md#amount) | required | Amount in currency which was used for the payment during the charge. i.e. currency that will be visible on the user bank statement for the payment. |
| `CreatedUtc` | string | required | Date and time of the payment creation in UTC timezone in ISO 8601 format. |
| `EnterpriseId` | string | required | Identifier of the enterprise receiving the payment. |
| `PaymentRequestId` | string | required | Identifier of the payment request. |
| `State` | string [Payment state](./operations.md#payment-state) | required | State of the payment attempt. |

#### Amount

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Currency` | string | required | ISO 4217 code of the currency. |
| `GrossValue` | number | required | Gross value of the amount. (Net + sum of `TaxValues`) |
| `NetValue` | number | required | Net value of the amount. |
| `TaxValues` | array of [Tax value](./operations.md#tax-value)s | required | Tax values of the amount. |

#### Payment state

- `Pending` - Non-finite state. Payment has been created, but the state is not known yet.
- `Verifying` - Non-finite state. Payment is awaiting a 3DS verification.
- `Charged` - Finite state. Payment has been successfully charged.
- `Canceled` - Finite state. Payment has been canceled, and it has not been charged.
- `Failed` - Finite state. Payment has not been charged.
