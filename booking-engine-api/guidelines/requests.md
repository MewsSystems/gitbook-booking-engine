# Requests

The API accepts only `HTTP POST` requests with `Content-Type` set to `application/json` and JSON content dependent on the operation to be performed. All operations follow this address pattern:

```text
[ApiBaseUrl]/api/distributor/v1/[Resource]/[Operation]
```

* **ApiBaseUrl**
  * Base address of the Mews Booking Engine API, this depends on the [Environment](environments.md) (Demo or Production).
* **Resource**
  * Logical group of operations, in most cases this identifies the target of the operation.
* **Operation**
  * Name of the operation to be performed.

## Request body

```json
{
    "Client": "My Client 1.0.0",
    "LanguageCode": null,
    "CultureCode": null 
}
```
| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `Client` | string | required | Identification of the Client as described in [Authorization](./authorization.md) |
| `LanguageCode` | string | optional | Code of the language |
| `CultureCode` | string | optional | Code of the culture |

* All API operations require `Client` to be present in the request.
* All API operations optionally accept `LanguageCode` and `CultureCode`. These can be used to enforce the language and culture of the operation, which affects for example the names of entities, descriptions or error messages.
Both of these values must be defined together, otherwise default values for the enterprise are used.
