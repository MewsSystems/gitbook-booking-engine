# FAQ

Here we address some Frequently Asked Questions concerning the Booking Engine Standalone integration.

* [Where can I get Configuration ID?](#where-can-i-get-configuration-id)
* [Why doesn't the Booking Engine use the Configuration IDs I've provided?](#why-doesnt-the-booking-engine-use-the-configuration-ids-ive-provided)
* [Where can I get City ID?](#where-can-i-get-city-id)

## Where can I get Configuration ID?

The Booking Engine Configuration ID is a unique identifier for your particular Booking Engine implementation. You can find it in __Mews Operations__.

* Start on the **Dashboard** (the main screen).
* In the left-hand menu, select **Settings** -> **Services**.
* In the section **Bookable services**, select the service which has the Booking Engine configuration. If there's just one service, select that one.
* On the left, select **Booking engines**.
* Select the configuration you want to use.
* In the upper section there is a field **Identifier**. This is your Configuration ID. It has the format `aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee`.

![configuration id in Mews Operations](../.gitbook/assets/commander-configuration-id.png)

## Why doesn't the Booking Engine use the Configuration IDs I've provided?

It could be that some of those ids are not valid configuration ids.

Please check that:
* All used configuration ids are really configuration ids, not chain, enterprise or other ids.
* All used configuration ids are defined in Commander PMS from the same [environment](../booking-engine-api/guidelines/environments.md) as the Distributor you are using.
* You are using only one configuration id per enterprise.

## Where can I get City ID?

You can find it in Commander PMS.

* Start on **Dashboard** (main) screen.
* In the left menu select **Settings** -> **Services**.
* In a section **Bookable services** select service which has the Distributor configuration which you use. If there's just one, try that one.
* On the left select **Booking engines**.
* Select configuration which you use.
* At the upper section you have field **City Identifier**. This is your city id. It has a format `aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee`.

![city id in Commander PMS](../.gitbook/assets/commander-city-id.png)
