# How to support payment cards in booking engine application

When creating a reservation it is possible to attach a payment card to the reservation.

As part of creating your own custom booking engine you may want to have a form within your client application where customers
can enter their payment card data and send this data to Distributor API for further use. Payment card data can then
be used by Mews for charging the customer.

To do that some Distributor API endpoints support or require [credit card data](../operations.md#credit-card-data)
in the request.

### Where to get `CreditCardData` values

* Confirm that **property supports PCI Proxy** by checking the field [payment card storage type](../operations.md#payment-card-storage-type) in Distributor API response. Also read docs about [payment gateway](../operations.md#payment-gateway) to see what other API data you could potentially use for your implementation.
* Use [PublicKey](../operations.md#payment-gateway) as `merchantId` while implementing PCI Proxy fields. Follow PCI Proxy [guide](https://docs.pci-proxy.com/collect-and-store-cards/capture-iframes) to handle the sensitive card data and obtain `PaymentGatewayData`.
  * PCI Proxy documentation only highlights the sandbox endpoints (used for staging environment). In production environment, you have to omit the `sandbox.` part from the address. For example `https://pay.sandbox.datatrans.com/upp/payment/js/secure-fields-2.0.0.min.js` then becomes `https://pay.datatrans.com/upp/payment/js/secure-fields-2.0.0.min.js` .
* PCI Proxy service will return you a `transactionId` in the response which will be used as `PaymentGatewayData` inside [credit card data](../operations.md#credit-card-data).
* Once you have the `PaymentGatewayData` you can create a payment card by providing [credit card data](../operations.md#credit-card-data) in a request body.

