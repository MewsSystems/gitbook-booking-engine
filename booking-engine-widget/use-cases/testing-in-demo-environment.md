# Testing Booking Engine Widget in Demo environment

The Booking Engine Widget uses production environment by default.

Before you are ready to run the Booking Engine Widget against real data, you can use the Booking Engine Widget with [Demo environment](../../booking engine-api/environments.md) data instead.

Most of the steps are the same as in [Getting started section](../getting-started.md).

The only difference is in the [initialization of the Booking Engine Widget](../getting-started.md#initialize-booking-engine-widget).

In comparison to the default example, you can set an [optional `dataBaseUrl`](../reference.md#string-databaseurl) property to the testing/staging API URL:

```javascript
Mews.Distributor(
    { configurationIds: ['aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee'] },
    function (api) {
        api.open();
    },
    { dataBaseUrl: 'https://api.mews-demo.com' }
);
```

Make sure you use `configurationIds` from the correct environment. Otherwise, the `configurationIds` [won't be used](../../faq.md#why-booking-engine-doesnt-use-the-configuration-ids-ive-provided).

After doing this, Booking Engine Widget will start using the data from [staging/testing environment](../../booking-engine-api/environments.md), instead of from the production.
