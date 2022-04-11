# Product pricing deprecation
`Amounts` and `RelativePrice` fields of [product](../operations.md#product) object is deprecated and will be removed from the response of [hotels/get](../operations.md#get-hotels) and [configurations/get](../operations.md#get-configuration). It is replaced by [Pricing](../operations.md#pricing).

## Response diff

```diff
{
    ...
    "Products": [
        {
            ...
-           "Amounts": {...},
-           "RelativePrice": 0.05,
+           "Pricing": {...},
        }
    ]
}
```
