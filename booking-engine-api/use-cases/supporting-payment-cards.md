# Supporting payment cards

When creating a reservation, it is possible to attach a payment card to the reservation.
As part of creating your own custom booking engine, you may want to have a form within your application where customers can enter their payment card data and send this data to the Booking Engine API for further use.
Payment card data can then be used by Mews for charging the customer.
To do that, some Booking Engine API operations support or require [Credit card data](../operations/reservation-groups.md#credit-card-data) in the request.

### Where to get `CreditCardData` values

* Confirm that the hotel or property supports PCI Proxy by checking the field [Payment card storage type](../operations/hotels.md#payment-card-storage-type) in the configuration data returned from [Get hotels](../operations/hotels.md#get-hotels).
Also refer to the [Payment gateway](../operations/hotels.md#payment-gateway) documentation to see what other API data you could potentially use for your implementation.
* Use [PublicKey](../operations/hotels.md#payment-gateway) as the `merchantId` while implementing PCI Proxy fields; and follow the [PCI Proxy guide](https://docs.pci-proxy.com/collect-and-store-cards/capture-iframes) to handle the sensitive card data and obtain `PaymentGatewayData`.
  * Note: PCI Proxy documentation only highlights the sandbox endpoints, used for the staging environment; in the production environment, you have to omit the `sandbox.` part from the address. For example, `https://pay.sandbox.datatrans.com/upp/payment/js/secure-fields-2.0.0.min.js` then becomes `https://pay.datatrans.com/upp/payment/js/secure-fields-2.0.0.min.js`.
* PCI Proxy service will return you a `transactionId` in the response which will be used as `PaymentGatewayData` inside [Credit card data](../operations/reservation-groups.md#credit-card-data).
* Once you have the `PaymentGatewayData`, you can create a payment card by providing [Credit card data](../operations/reservation-groups.md#credit-card-data) in the request body.

