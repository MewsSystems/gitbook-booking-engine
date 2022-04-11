# Average amount per night deprecation
`AverageAmountPerNight` field of [room price](../operations.md#room-price) object is deprecated and will be removed from the response of [hotels/getAvailability](../operations.md#get-availability) and [reservations/getPricing](../operations.md#get-reservations-pricing). It is replaced by `AverageAmountPerTimeUnit`.

## Response diff

```diff
{
    ...
    "Price": [
        {
            ...
-           "AverageAmountPerNight": { },
+           "AverageAmountPerTimeUnit": { },
        }
    ]
}
```
