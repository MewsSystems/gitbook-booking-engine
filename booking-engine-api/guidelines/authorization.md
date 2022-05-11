# Authorization

The Mews Booking Engine API is a public API with client name authorization. It is sufficient to know the unique identifier of a hotel in order to access it, however it is required that the client identify itself by providing the `Client` property in all requests made to the API.

The Client application needs to be pre-registered with Mews Support at `support@mews.com`. The registration request should contain:

* `Client`  - the name of the client that will be used for every API request
* `Email` -  an email contact for the client's tech/dev department; this email will be used by our developers in order to notify you about any breaking changes in the API
* `Environments` - we offer two [environments](./environments.md), `Production` and `Demo`, where `Demo` should be used during API implementation. **Note:** the two environments have separate client lists, so make sure you are registered in `Production` before you move your implementation to the Production environment.

> **Sample Client name**
> 
> Before the registration of your Client name is confirmed, you can use the sample Client name below. This Client name will **only work in the Demo environment**.
> Keep in mind that this must be replaced by your proper Client name as soon as you finish the registration process.
>
>```json
>{
>    "Client": "My Client 1.0.0"
>}
>```
