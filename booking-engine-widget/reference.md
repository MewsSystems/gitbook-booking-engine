# Reference

## Options reference

> **Note:**
>
> Direct configuration of Distributor through the options has been deprecated and it will be disabled in future. Prefer to use Distributor Configuration in Commander. The only supported now are`configurationIds`and`openElements`.

| Name | Type | Default value | Description |
| :--- | :--- | :--- | :--- |
| configurationIds \(required\) | array of`string` | `''` | Unique identifier of the used Distributor configurations.  You can get unique identifier of a configuration from it’s details page in Commander. The unique identifier is shown there as Identifier. |
| openElements | `string` | `''` | A list of comma-separated CSS selectors of elements, which will automatically get attached click event listeners for opening Distributor. The string is given as an argument to the`document.querySelectorAll`function, you get more info about its resemblance[here](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll)for example.  The click event is being delegated, meaning that each element is being looked up on a website dynamically after the click happens. This way you can pass a selector to the elements that don’t exist yet during the initialization. |

## API reference

API calls are defined on the Distributor instance, which is created with the initialization call. This instance is returned to you as an argument of a callback function that you can pass as the second parameter to the initialization call. The following simple example shows how to use the calls to set up start and end dates, and then open the Distributor:

```javascript
<!-- Example of use of an instance to call the API -->
<script>
Mews.Distributor({
    configurationIds: ['aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee'],
}, function(distributor) {
   $('.booking-button').click(function() {
     var start = new Date();
     var end = new Date();
     end.setDate(start.getDate() + 2);

     distributor.setStartDate(start);
     distributor.setEndDate(end);
     distributor.open();
   });
});
</script>
```

Beware that API is slightly different in the\_Single\_and the\_Chain\_modes. The list of all API calls follows:

### Common API calls <a id="common-api-calls"></a>

#### open\(\) <a id="open"></a>

Opens Distributor in its overlay.

#### close\(\) <a id="close"></a>

Closes Distributor and its overlay. Even though Distributor is closed, it still responds to API calls.

#### setLanguageCode\(languageCode\) <a id="setlanguagecodelanguagecode"></a>

* `languageCode` Type: `string` - The languageCode to be set, in format `language-countryCode`, i.e`en-US`

Sets language of the Distributor’s localization. Language code should be in format`language-countryCode`, i.e.`en-US`as a variant of [IETF tag](https://en.wikipedia.org/wiki/IETF_language_tag). If a`languageCode`is not a in valid format, nothing happens.

#### setCurrencyCode\(currencyCode\) <a id="setcurrencycode"></a>

* `currencyCode` Type: `string` - The currencyCode to be set, in [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) format, i.e`EUR`

Sets currency of the Distributor’s localization. Currency code should be in [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) format. If a`currencyCode` is not a in valid format, nothing happens.

#### setStartDate\(date\) <a id="setstartdatedate"></a>

* `date` Type: `Date` - The start date to set

Sets start date for a new availability query, currently loaded availability list is not affected. If a `date` is not a valid Date object or its value isn’t allowed as start date - nothing happens.

`monthIndex` starts with `0` for January to `11` for December - ([click here for more details](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/Date#Individual_date_and_time_component_values)).

* Example - good (18 January 2019):

```javascript
distributor.setStartDate(new Date(2019, 0, 18))
```

* Example - wrong:

```javascript
distributor.setStartDate("2019-01-18")
```

#### setEndDate\(date\) <a id="setenddatedate"></a>

* `date` Type: `Date` - The end date to set

Sets end date for a new availability query, currently loaded availability list is not affected. If a `date` is not a valid Date object - nothing happens.

`monthIndex` starts with `0` for January to `11` for December - ([click here for more details](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/Date#Individual_date_and_time_component_values)).

* Example - good (18 December 2019):

```javascript
distributor.setEndDate(new Date(2019, 11, 18))
```

* Example - wrong:

```javascript
distributor.setEndDate("2019-12-18")
```

#### setVoucherCode\(code\) <a id="setvouchercodecode"></a>

* `code` Type: `string` - The voucher code to set

Sets a new voucher code value.

#### setAdultCount\(adultCount\)

* `adultCount` Type: `number` - number of adults to set

Sets the number of adults that should be selected by default. Space occupancy for adults on rate screen will be pre-filled according to this value.

#### setChildCount\(childCount\)

* `childCount` Type: `number` - number of children to set

Sets the number of children that should be selected by default. Space occupancy for children on rate screen will be pre-filled according to this value.

#### disableTracking()

Sets all [TrackingConsents](integrations.md#trackingconsents) to false.

#### enableTracking()

Sets all [TrackingConsents](integrations.md#trackingconsents) to true.

### Only Single mode API calls <a id="only-single-mode-api-calls"></a>

#### showRooms\(\) <a id="showrooms"></a>

Sets Distributor to the`Rooms`step.

#### showRates\(roomId\) <a id="showratesroomid"></a>

* `roomId` Type: `string` - an ID of a room to be selected

Sets Distributor to the third step \(`Rates`\) as if you selected a room on the second screen.

### Only Chain mode API calls <a id="only-chain-mode-api-calls"></a>

#### showHotels\(\) <a id="showhotels"></a>

Sets Distributor to the`Hotels`step.

#### showRooms\(hotelId\) <a id="showroomshotelid"></a>

* `hotelId` Type: `string` - an ID of a hotel which rooms you want to display

Sets Distributor to the`Rooms`step.

#### setCity\(cityId\)

* `cityId` Type: `string` - an ID of a city which hotels you want to display

### \(Optional\) Advanced configuration

As the third parameter, `Mews.Distributor` accepts optional configuration.

```javascript
Mews.Distributor(
    { configurationIds: ['aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee'] },
    function (api) {
        api.open();
    },
    { dataBaseUrl: 'https://api.mews-demo.com' }
);
```

#### string dataBaseUrl

Allows you to define custom URL which is used for distributor API calls and static assets. In the example above, the Distributor will be run against our Demo environment.
