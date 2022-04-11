# Product posting deprecation
`Posting` field of [product](../operations.md#product) object is deprecated and will be removed from the response of [hotels/get](../operations.md#get-hotels) and [configurations/get](../operations.md#get-configuration). It is replaced by [Product posting mode](../operations.md#product-posting-mode).

## Response diff

```diff
{
    ...
    "Products": [
        {
            ...
-           "Posting": "Daily",
+           "PostingMode": "PerTimeUnit",
        }
    ]
}
```
