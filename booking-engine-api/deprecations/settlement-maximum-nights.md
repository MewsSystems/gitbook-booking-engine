# SettlementMaximumNights deprecation
`SettlementMaximumNights` field of [rate group](../operations.md#rate-group) object is deprecated and will be removed from the response of [hotels/getAvailability](../operations.md#get-availability). It is replaced by `SettlementMaximumTimeUnits`.

## Response diff

```diff
{
    ...
    "RateGroups": [
        {
            ...
-           "SettlementMaximumNights": 1,
+           "SettlementMaximumTimeUnits": 1,
        }
    ]
}
```
