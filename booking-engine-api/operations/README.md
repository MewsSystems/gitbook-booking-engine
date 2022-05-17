# API Operations

This section describes all operations supported by the API, organised by theme.

## Availability

| <div style="width:200px">Operation or Endpoint</div> | Description |
| :-- | :-- |
| [Get availability](hotels.md#get-availability) | Gives availabilities and pricings for given date interval with product prices included for each room category. Categorized by applicable rates and person counts from 1 to full room. If room category is not available, it is left out from response |

## Configuration

| <div style="width:200px">Operation or Endpoint</div> | Description |
| :-- | :-- |
| [Get configuration](configuration.md#get-configuration) | Preferred initial call used to obtain all static data about distributor configuration for the client |
| [Get hotels](hotels.md#get-hotels) | Alternative initial call used to obtain all static data about hotel relevant for the client |
| [Get payment configuration](hotels.md#get-payment-configuration) | ??? |

## Payment cards

| <div style="width:200px">Operation or Endpoint</div> | Description |
| :-- | :-- |
| [Get payment cards](payment-cards.md#get-payment-cards) | Fetch details about the listed payment cards, in particular the Authorization state. |
| [Authorize payment card](payment-cards.md#authorize-payment-card) | Request authorization of the given payment card. |

## Reservations

| <div style="width:200px">Operation or Endpoint</div> | Description |
| :-- | :-- |
| [Get reservations pricing](reservations.md#get-reservations-pricing) | ??? |
| [Create reservation group](reservation-groups.md#create-reservation-group) | ??? |
| [Get reservation group](reservation-groups.md#get-reservation-group) | ??? |

## Vouchers

| <div style="width:200px">Operation or Endpoint</div> | Description |
| :-- | :-- |
| [Validate voucher](vouchers.md#validate-voucher) | Can be used to determine whether a voucher code is valid |
