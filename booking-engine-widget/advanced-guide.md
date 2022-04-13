# Advanced Guide

## Full example

> **Note:**
>
> Direct configuration of Distributor through the options has been deprecated and it will be disabled in future. Prefer to use Distributor Configuration in Commander. The only supported now are`configurationIds`and`openElements`.

Example with all possible options and their default values follows. To get further information about the options and an API call, see the [reference](reference.md).

**Important: This is just an example, do not copy this directly to your website!**

```javascript
<script>
Mews.Distributor({
    // required
    configurationIds: [
        'aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee'
    ],
    // optionals
    openElements: '',
},
function(distributor) {
    // Always available api calls
    // distributor.open();
    // distributor.setLanguageCode(languageCode);
    // distributor.setCurrencyCode(currencyCode);
    // distributor.setStartDate(date);
    // distributor.setEndDate(date);
    // distributor.setVoucherCode(code);
    // distributor.setRooms(rooms);
    // Singlehotel mode api calls
    // distributor.showRooms();
    // distributor.showRates(roomId);
    // Multihotel mode api calls
    // distributor.showHotels();
    // distributor.showRooms(hotelId);
    // distributor.setCity(cityId);
});
</script>
```

#### Note  <a id="note-1"></a>

See that you have just one`<script>`tag containing`Mews.Distributor`call on your page.

### Payment card storages

Payment card storage is used to safely collect and store information about a customer's payment card. Currently Distributor supports these payment card storages:

* [PCI Proxy](https://www.pci-proxy.com)

### Payment gateways

Payment gateway is used to securely handle customer payments. A configuration is done once, when the property is set up. Official Mews Distributor client can use it with minimal setup. Currently Distributor supports these payment gateways:

* [Mews Payments](https://www.mews.com/en/products/payments)

Using payment gateway is not mandatory, as reservations can be created without providing a payment card information.

> **Important:** PCI Security Standard requires you to use **SSL Certificate** on your website to be allowed to collect any payments info.

