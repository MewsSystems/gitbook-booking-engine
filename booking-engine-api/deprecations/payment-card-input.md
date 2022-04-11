# PaymentCardInput deprecation
`PaymentCardInput` field of [configuration](../operations.md#configuration) object is deprecated and will be removed from the response of [configuration/get](../operations.md#get-configuration). It is replaced by [Payment card requirement](../operations.md#payment-card-requirement).

## Response diff

```diff
{
    ...
    "Configurations": [
        {
            ...
-           "PaymentCardInput": "NotRequested",
+           "PaymentCardRequirement": "NotRequired",
        }
    ]
}
```
