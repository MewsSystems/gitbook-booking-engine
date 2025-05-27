# Authentication

The __Mews Booking Engine API__ is a public API that requires client authentication and authorization. 

## Client authentication

Authentication is the process of verifying the identity of the client. To access the API, you must include the `Client` property in every request. This value identifies your client application and must match a pre-registered name in Mews.

> **Client name:** In our documentation, we refer to the pre-registered name as your `client name`. It corresponds to the `Client` property in the API payload.

### Registration

Before using your own `client name` in requests, it must be registered with Mews. You will also need to provide a contact email address for your development team. This email will be used to notify you of any important API updates or breaking changes.

#### Recommended: Use the Mews Digital Assistant

Register from within Mews Operations using the **Mews Digital Assistant** chatbot (available to logged-in users):  
[How to use the Mews Digital Assistant](https://help.mews.com/s/article/How-to-use-the-Mews-Digital-Assistant)

Provide the following details:

* `Client name`: the application name you will use in the `Client` property for every API request
* `Contact email`: your development contact email
* `Environments`: `Demo` and/or `Production`

#### Alternatively: Register by email

If you don’t have access to the Digital Assistant, email [support@mews.com](mailto:support@mews.com) with the same information.

### Environments

We offer two environments:

- `Demo`: for testing and development
- `Production`: for live customer sites

Each environment maintains a separate list of registered `client names`. Ensure your `client name` is registered in each environment you plan to use. See [Environments](environments.md) for details.

### Sample client name

While your `client name` is being registered, you can begin development using the following sample value:

```json
{
    "Client": "My Client 1.0.0"
}
```

>️ **Only for Demo**: This sample `client name` is only valid in the Demo environment and should be replaced once registration is complete.

## Client authorization

Authorization determines what an authenticated client is allowed to do. In this API, access is granted based on the `Client` property and a known enterprise identifier. As long as your `client name` is registered and included in the `Client` property, and you have the correct enterprise identifier, the API will authorize your request.
