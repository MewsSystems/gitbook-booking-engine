# Guidelines

## Usage

The __Mews Booking Engine API__ is a public API with client name authorization. It is designed to be consumed directly by frontend clients. It is unsuitable for continuous polling by a single server due to the built in anti-scraping protection and such requests can fail. For server to server communication, please refer to the [Mews Connector API](https://mews-systems.gitbook.io/connector-api/).

## Requests

The API accepts only `HTTP POST` requests with `Content-Type` set to `application/json` and JSON content depending on the operation to be performed. All operations follow this address pattern:

```text
[ApiBaseUrl]/api/distributor/v1/[Resource]/[Operation]
```

* **ApiBaseUrl**
  * Base address of the Mews Booking Engine API, this depends on the [environment](environments.md) (Demo or Production).
* **Resource**
  * Logical group of operations, in most cases this identifies the target of the operation.
* **Operation**
  * Name of the operation to be performed.

### Body
```json
{
    "Client": "My Client 1.0.0",
    "LanguageCode": null,
    "CultureCode": null 
}
```
| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `Client` | string | required | Identification of the client as described in [authorization](./authorization.md). |
| `LanguageCode` | string | optional | Code of the language. |
| `CultureCode` | string | optional | Code of the culture. |

All operations of the API require `Client` to be present in the request.
All operations of the API optionally accept `LanguageCode` and `CultureCode`. These can be used to enforce language and culture of the operation which affects, for example, the names of entities, descriptions or error messages.
Both of these values must be defined together, otherwise default values of the enterprise are used.

## Responses

The API responds with `Content-Type` set to `application/json` and JSON content. In case of success, the HTTP status code is 200 and the content contains results according to the call.
In case of error, there are multiple HTTP status codes for different types of errors:

* **400 Bad Request**
  * Error caused by the client app, e.g. in case of malformed request or invalid identifier of a resource. In most cases, such an error signifies an error in the client application, i.e. the consumer of the API.
* **401 Unauthorized**
  * Error caused by usage of invalid access token.
* **403 Forbidden**
  * Server error that should be reported to the end user of the client application. This happens, for example, when the server-side validation fails or when a business-logic check is violated.
* **500 Internal Server Error**
  * Unexpectced error of the server. In most cases, such an error signifies an error on the Mews side. This will be logged and we will be notified immediately when such an error occurs.
  If anything like this happens, feel free to contact Mews directly or raise an issue on GitHub.

In case of any error, the returned JSON object describes the error and has the following properties:

| Property | Type | Contract | Description |
| :--- | :--- | :--- | :--- |
| `Message` | string | required | Description of the error. |
| `Details` | string | optional | Additional details about the error \(request, headers, server stack trace, inner exceptions, etc.\). Only available on Development environment. |

Some errors may also contain additional information relevant to the error on top of these two properties, but that depends on the operation and is specifically described in the operation documentation.
