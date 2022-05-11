# On session payments

Whenever a user creates a reservation, there is an option to allow them to pay directly. This needs to be correctly configured via
settlement rules on `RateGroup`. We provide this functionality only for `Rates` where the payment card is charged
automatically at the time of creating the reservation. In order to simplify the whole payment processing workflow
we offer this functionality in our applications via a feature called "Payment request".

## Creating a reservation group

The first step of the entire workflow is to [create a reservation group](../operations/reservation-groups.md#create-reservation-group) via the API.
The response contains a field `PaymentRequestId` which we will use for a redirect to an application that can handle the payment.
The payment gateway supports an optional query parameter `returnUrl` which will be used to return the user into your booking engine after successful payment or in case the user decides to abandon the flow.
The `returnUrl` value should be a Base64-encoded absolute URL, e.g. in JavaScript via the `btoa` function.
After the user returns to your booking engine, you can verify the state of the payment request by calling [get reservation group](../operations/reservation-groups.md#get-reservation-group) with `Extent` for `PaymentRequests` and optionally for `Payments` which you want to validate.
Validation should be done mainly on the [payment request state](../operations.md#payment-request-state) and optionally [payment state](../operations.md#payment-state).

## Step by step workflow
1. [Create new reservation group](../operations.md#create-reservation-group).
2. Get `PaymentRequestId` from the response.
3. Create a `ReturnUrl` via encoding your url by `Base64` e.g. JavaScript example would be `btoa(urlWhereUserShouldReturn)`.  
4. Redirect the user to the gateway on url `https://[MewsApplicationsBaseUrl]/navigator/payment-requests/detail/[PaymentRequestId]?returnUrl=[ReturnUrl]`. You can find out the `MewsApplicationBaseUrl` in [environments](../environments.md) section.  
5. After the user returns to the `ReturnUrl` in your booking engine you can verify the state by using [reservation group detail](../operations.md#get-reservation-group) with a specified [reservation group extent](../operations.md#reservation-group-extent).  
6. Validate the state of the Payment request in the response.

> **Note:** Until the Payment request enters its [finite state](../operations.md#payment-request-state) you can redirect the user again, for example with a "Try to pay again" button.
