# Product charging deprecation
`Charging` field of [product](../operations.md#product) object is deprecated and will be removed from the response of [hotels/get](../operations.md#get-hotels) and [configurations/get](../operations.md#get-configuration). It is replaced by [Product charging mode](../operations.md#product-charging-mode).

## Response diff

```diff
{
    ...
    "Products": [
        {
            ...
-           "Charging": "PerRoomNight",
+           "ChargingMode": "PerTimeUnit",
        }
    ]
}
```
