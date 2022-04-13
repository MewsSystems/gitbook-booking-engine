# Testing Booking Engine Widget in Demo environment

The Booking Engine Widget uses the Production environment by default.
Before you are ready to run the Booking Engine Widget against real data, you should use the Booking Engine Widget with [Demo environment](../../booking engine-api/environments.md) data instead.
Most of the steps are the same as in the [Getting started](../getting-started.md) section.

The only difference is in [Step 2: Initialize Booking Engine Widget](../getting-started.md#step-2-initialize-booking-engine-widget).

In comparison to the default example, you can set an [optional `dataBaseUrl`](../reference.md#string-databaseurl) property to the Demo environment API URL:

```javascript
Mews.Distributor(
    { configurationIds: ['aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee'] },
    function (api) {
        api.open();
    },
    { dataBaseUrl: 'https://api.mews-demo.com' }
);
```

Make sure you use `Configuration IDs` from the correct environment. Otherwise, the `Configuration IDs` [won't be used](../../faq.md#why-booking-engine-doesnt-use-the-configuration-ids-ive-provided).

After doing this, Booking Engine Widget will start using the data from [Demo environment](../../booking-engine-api/environments.md), instead of from the Production.
