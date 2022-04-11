# Authorization

The Distributor API is a public API with client name authorization. It suffices to know unique identifier of a hotel in order to access it. However it is required that the client would identify itself by providing the `Client` property in all requests made to the API. The `Client` needs to be registered via our support at `support@mews.com`.

The registration request should contain:

* `Client` name of the client that will be used for every request during the API communication
* `Email` email contact for a tech/dev department. This email will be used by our developers in order to notify about breaking changes in the API.
* `Environments` We offer two [environments](./environments.md) `Production` & `Demo` where `Demo` should be used during the API implementation. **Those two environments does have a separate list so make sure to be registered in `Production` before you move your implementation to production environment.**

{% hint style="info" %}
Before the registration of your **Client** is confirmed you can use a sample client name from example below. **This client name will work only in Demo environment**. But keep in mind that this should be replaced by your client as soon as you finish the registration process.

```json
{
    "Client": "My Client 1.0.0"
}
```
{% endhint %}

## Where to go next

You can start your first request in our [operations section](./operations.md).

