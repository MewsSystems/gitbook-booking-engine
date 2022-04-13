# Integrations

## Google Tag Manager

> ### Notice of usage
> Google Tag Manager is a 3rd party service and we provide this integration as is. We export a set of supported events and their data to the container, however, we have no control over what happens with them and how they are used. Below we provide a set of basic setup examples that have been tested and verified to work with Distributor. If you need a more complex setup, it is up to you to configure and test it.

This guide assumes at least basic knowledge of [Google Tag Manager](https://www.google.com/analytics/tag-manager/) - how to create and publish a container, how to setup a triggers and custom events and how to connect them to a tags.

### Enabling Google Tag Manager in Distributor

You can enable it by setting up your GTM container’s id in the Distributor's configuration in Mews Commander. The id has format`GTM-XXXXXX` and you can find it in Google Tag Manager.

> Important: It is not enough to just copy and paste the Google Tag Manager container code to a website, you have to set it up in the configuration. However, if you use the container on your website, Distributor will connect to it and will not create a new one.

### Migrating to Google Tag Manager

In previous versions, Distributor supported direct integrations with Google Analytics and Google AdWords. These legacy integrations still remain functional for a backward compatibility, but will be removed completely in the near future. We strongly suggest you migrate them to Google Tag Manager.

> Important: If you enable Google Tag Manager in Distributor, it will take precedence over any legacy integration, and those will not be triggered. Meaning that once you enable Google Tag Manager, you will have to migrate all of your integrations to it!

### Triggers

This is a basic description of how to set up a Distributor event as a Trigger. You can get full reference of all Distributor events [here](./integrations.md#triggers-reference).

For an integration with Google Tag Manager, Distributor provides a set of _Custom Events \_that you can set up as_ Triggers\_. To setup a Trigger for an event, match it with its name:

![trigger](../.gitbook/assets/trigger.png)

If you want to track multiple events with one Trigger, you can easily use regex matching on an event name. For example`^distributor`will track every distributor event, which can be useful for setting a Trigger for Universal Analytics:

![regex trigger](../.gitbook/assets/triggerregex.png)

### Basic setups

#### Universal Analytics

You can track all the events for further statistical computations about behaviour of your customers. Use the Google Universal Analytics tag with the`Event`track type. The Trigger should be a regex grouping of all the events you want to track \(to track all events, you can use`^distributor`regex as described [here](./integrations.md#triggers)\).

![events\_tag](../.gitbook/assets/eventstag.png)

#### Google Ecommerce

You can track transactions with the Google Universal Analytics tag with the`Transaction`track type on the`distributorBookingFinished`event. All the needed data for tracking is set in the Tag Manager’s _dataLayer_ and will be passed automatically.

Each reservation is send as _Product_ with quantity set to 1. Name of the reserved category is send as _Product name_, name of the hotel is send as _Product category_.

![ecommerce\_tag](../.gitbook/assets/ecommercetag.png)

#### Google Enhanced Ecommerce

We also publish all interesting data for enhanced ecommerce tracking. To track these, setup a tag with `Enable overriding settings in this tag` option enabled, then under More Settings &gt; Ecommerce set option `Enable Enhanced Ecommerce Features` to `True` and check `Use Data Layer`. The trigger should be set to all distributor events as described previously.

Track Type of the event shouldn't be important in this case. You can even reuse the same tag as for tracking all distributor events in analytics.

Be sure to also enable Enhanced Ecommerce in you Google Analytics under Admin &gt; Ecommerce settings. The Enhanced Ecommerce plug-in should not be used alongside the Ecommerce plug-in for the same property.

![](../.gitbook/assets/image.png)

**Tracking with Mews Merchant and source attribution**

When you have Mews Merchant set up, a payment by a customer is legally required to happen on our domain. Therefore, all the transactions during a checkout are attributed to Mews domain. This is an unfortunate limitation of the checkout process that we cannot currently overcome.

### Conditionally firing tags based on tracking consents

Google Tag Manager integrations are very often used to track users, be it with cookies or other approaches. You can use [TrackingConsents](./integrations.md#trackingconsents) and Google Tag Manager to use integrations only when permitted.
A commonly used integration which often needs a tracking consent is Universal Analytics.
Let's see how you can fire Universal Analytics tag only when [TrackingConsents](./integrations.md#trackingconsents) permit it.

1. **Set up Universal Analytics in Google Tag Manager**
	* See previous section about [Universal Analytics](./integrations.md#universal-analytics).

2. **Let Distributor know what the tracking consents should be**
	* Call Distributor API methods [enableTracking](./reference.md#enabletracking) or [disableTracking](./reference.md#disabletracking) when the Distributor widget starts.
	* Calling the API methods at the start guarantees all events have the correct consents.
	* Don't rely on defaults since they can be changed in the future. Defaults are there only for backwards compatibility.
	* You can also call mentioned API calls again later, e.g. after user agrees with tracking in your cookie banner.

3. **Create data layer variable for performance tracking consent**
	* Open Google Tag Manager.
	* Go to "Variables" section.
	* Click "New".
	* Name the variable - e.g. `performanceConsent`.
	* Select "Variable Type" to be "Data Layer Variable".
	* Set the "Data Layer Variable Name" to `trackingConsents.performance`.
	* Click "Save".

4. **Create trigger for all distributor events where performance consent is given/true**
	* Go to "Triggers".
	* Click "New".
	* Name the trigger - e.g. "All Distributor events with performance consent".
	* Select trigger type "Custom Event".
	* Inside "Event name" add `^distributor`.
	* Tick "Use regex matching".
	* Select "Some Custom Events".
	* Select condition `performanceConsent equals true`.
	* Click "Save".

5. **Use created trigger to fire Universal Analytics tag**
	* Go to "Tags".
	* Click Universal Analytics tag.
	* Click inside "Triggering" section.
	* Remove previous trigger/s for distributor events if there are any.
	* Add trigger "All Distributor events with performance consent".
	* Click "Save".

6. **All is set up now**
	* Preview or submit your changes. 
	* From now on, Universal Analytics will fire only when the performance consent is given.

### Troubleshooting

#### There are no events or ecommerce transactions tracked after a redirect to the Mews Merchant page

You have probably included the container in your website, however, you haven’t set the container id in Distributor. Meaning that after the redirect, Distributor will not know anything about your container. You should set up your GTM container’s id in the Distributor's configuration in Mews Commander.

#### I’ve set up the container correctly but there are still no events tracked

If you have everything set up correctly and you still cannot see events tracked, please, ensure that you’re not using any ad-blocking or similar software in your browser. They tend to block not only ads, but also tracking software like Google Tag Manager. Disabling the software for testing or adding your website to the exceptions should solve the issue.

> Important: If you are using Mews Payments, you need to disable the software for the \*.mews.com domain too.

#### The Tag Assistant Chrome extension shows me a warning about multiple installations, but I use only one

Distributor includes our Mews Google Tag Manager container \(id`GTM-M7JV35D`\) to keep statistics in our own Google Analytics. We use that data for a global Distributor performance measuring, to have an idea about performance in hotels that don’t use Analytics and for the ability to build our own statistics on top of the Analytics API in Commander.

Having multiple installations is perfectly fine, if you keep common data layer name for all of them, which we do. Please, see the official documentation: [https://developers.google.com/tag-manager/devguide\#multiple-containers](https://developers.google.com/tag-manager/devguide#multiple-containers)

| Next |
| :-- |
| [Triggers Reference](triggers-reference.md) |
