# Availability blocks

## How to obtain availabilityBlockId
In Mews Operations you generate availability block in desired property. From the user interface you get `availabilityBlockId` that can be used with some of yours booking engine configurations.

## How to work with availability blocks
- In your application, after you receive details about your availability block via [Get Availability blocks](../operations/availability-blocks.md#get-availability-blocks) you need to check if current date is between `StartUtc` and `EndUtc` interval. Otherwise, you can display, that availability block already expired.
- Then in your custom Booking Engine, you must provide `availabilityBlockId` into all endpoints, that accepts it.
- Filter [Rates](../operations/hotels.md#rate) with received availability block `rateId`. Only this Rate should available and bookable for this booking engine session.

### Endpoints accepting `availabilityBlockId`:
- [Get availability](../operations/hotels.md#get-availability)
- [Get reservations pricing](../operations/reservations.md#get-reservations-pricing)
- [Create reservation group](../operations/reservation-groups.md#create-reservation-group)
