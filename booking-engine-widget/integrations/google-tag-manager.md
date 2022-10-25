# Google Tag Manager (GTM)

> **Notice of usage:** Google Tag Manager (GTM) is a third party service and we provide this integration as is. We export a set of supported events and their data to the container, however, we have no control over what happens to them and how they are used. Below we provide a set of basic setup examples that have been tested and verified to work with the Mews Booking Engine. If you need a more complex setup, it is up to you to configure and test it and we recommend to ask specialist to set it up for you.

This guide assumes you have at least a basic knowledge of [Google Tag Manager](https://www.google.com/analytics/tag-manager/) - how to create and publish a container, how to set up triggers, custom events and variables and how to connect them to tags.

## Important links
[Google Tag Manager support](https://support.google.com/tagmanager/)
[Google Analytics support](https://support.google.com/analytics/)


## Enabling Google Tag Manager in Mews Booking Engine

You can enable Google Tag Manager (GTM) by setting up your GTM container ID in the booking engine's configuration in __Mews Operations__.
The ID has format `GTM-XXXXXX` and you can find it in Google Tag Manager.

> **Important:** It is not enough to just copy and paste the GTM container code to a website, you have to set it up in the configuration of the Google Tag manager.
> However, if you use the container on your website, Mews Booking Engine will connect to it and will not create a new one.

## Basic setup

### Tracking page-views with with Google Analytics 4 (GA4)

This is a basic description of how to set up tracking of page-views via Google Analytics 4 (GA4) in Mews Booking engine.

#### Create trigger for Mews booking engine events

For tracking of all screens you can set one trigger with value `^ga4` which will track all events within Mews Booking engine. Do not forget to check on checkbox `Use regex matching`.

> For a full list of events and e-commerce events, see the [Google Triggers Reference](google-triggers-reference.md).

![GTM trigger](../../.gitbook/assets/1.png)

#### Create variables for Location and Title

To dynamically set name and URL of tracked page-view, each event triggered in Mews Booking engine contains parameters `page_title` and `page_location`. You will need to create two custom variables in GTM so you can use them later in next step to send data to google Analytics.

![GTM Page Title variable](../../.gitbook/assets/2a.png)
![GTM Page Location variable](../../.gitbook/assets/2b.png)

#### Create Google Analytics 4 Tag

Once you have a trigger and variables set, you can set the `Google Analytics: GA4 configuration` tag.

1. Create a new tag - choose the `Google Analytics: GA4 configuration` type of tag
2. Add your Google Analytics 4 `Measurement ID` which you will find in the Google Analytics
3. Add `Fields to set` - create two fields for `page_title` and `page_location`. Use the two custom variables created in the previous step to fetch the location and title from datalayer automatically
4. Save and publish the tag and configuration

![GTM Page Location variable](../../.gitbook/assets/3.png)

After correct setup you will get all the screens users go trough in Mews Booking engine with URLs as well with correct page titles

### Google Analytics 4 eCommerce and custom events

In Universal analytics eCommerce was working automatically, but in the GA4 you need to create and configure all triggers / variables / tags manually. Follow Google Analytics official guide on how to set it. [Google Analytics - eCommerce support](https://support.google.com/analytics/answer/12200568?hl=en#zippy=%2Cgoogle-tag-manager-websites)

Mews booking engine fires following GA4 eCommerce events. Naming of the events is same as standard Google recommendation.

* view_item_list
* select_promotion
* add_to_cart
* remove_from_cart
* begin_checkout
* add_payment_info
* purchase

All the events contain additional data in Data layer that you can use to set up tracking according to your needs.

> For a full list of events and e-commerce events and data layer values, see the [Google Triggers Reference](google-triggers-reference.md).

### Conditionally firing tags based on tracking consents

Google Tag Manager integrations are very often used to track users, be it with cookies or other approaches. You can use [Tracking Consents](google-triggers-reference.md#trackingconsents) and Google Tag Manager to use integrations only when permitted.
A commonly used integration which often needs a tracking consent is Universal Analytics.
Let's see how you can fire Universal Analytics tag only when [Tracking Consents](google-triggers-reference.md#trackingconsents) permit it.

1. **Set up Universal Analytics in Google Tag Manager**
	* See previous section about [Universal Analytics](#universal-analytics)

2. **Let Mews Booking Engine know what the tracking consents should be**
	* Call the Javascript API methods [enableTracking](../reference.md#enabletracking) or [disableTracking](../reference.md#disabletracking) when the Booking Engine Widget starts
	* Calling the Javascript API methods at the start guarantees all events have the correct consents
	* Don't rely on defaults, since they can be changed in the future; defaults are there only for backwards compatibility
	* You can also call mentioned Javascript API functions again later, e.g. after the user agrees with tracking in your cookie banner

3. **Create data layer variable for performance tracking consent**
	* Open Google Tag Manager
	* Go to "Variables" section
	* Click "New"
	* Name the variable, e.g. `performanceConsent`
	* Select "Variable Type" to be "Data Layer Variable"
	* Set the "Data Layer Variable Name" to `trackingConsents.performance`
	* Click "Save"

4. **Create trigger for all booking engine events where performance consent is given/true**
	* Go to "Triggers"
	* Click "New"
	* Name the trigger, e.g. "All Booking Engine events with performance consent"
	* Select trigger type "Custom Event"
	* Inside "Event name" add `^distributor`
	* Tick "Use regex matching"
	* Select "Some Custom Events"
	* Select condition `performanceConsent equals true`
	* Click "Save"

5. **Use created trigger to fire Universal Analytics tag**
	* Go to "Tags"
	* Click Universal Analytics tag
	* Click inside "Triggering" section
	* Remove previous trigger(s) for booking engine events if there are any
	* Add trigger "All Booking Engine events with performance consent"
	* Click "Save"

6. **All set up!**
	* Preview or submit your changes
	* From now on, Universal Analytics will fire only when the performance consent is given

## Universal analytics setup (Legacy - Google will deprecate UA on 1.7.2023)

### Universal Analytics

You can track all the events for further statistical computations about behaviour of your customers. Use the Google Universal Analytics tag with the `Event` track type.
The Trigger should be a regex grouping of all the events you want to track \(to track all events, you can use `^distributor` regex, as described above\).

![events\_tag](../../.gitbook/assets/eventstag.png)

### Google Ecommerce (Legacy - Google will deprecate UA in 1.7.2023)

You can track transactions with the Google Universal Analytics tag using the `Transaction` track type on the `distributorBookingFinished` event.
All the data needed for tracking is set in the Tag Manager’s _data layer_ and will be passed automatically.

Each reservation is sent as _Product_ with quantity set to 1; the name of the reserved category is sent as _Product name_; the name of the hotel is sent as _Product category_.

![ecommerce\_tag](../../.gitbook/assets/ecommercetag.png)

### Google Enhanced Ecommerce

We also publish all interesting data for enhanced e-commerce tracking. To track these, set up a tag with the `Enable overriding settings in this tag` option enabled, then under **More Settings &gt; Ecommerce**, set option `Enable Enhanced Ecommerce Features` to `True` and check `Use Data Layer`. The trigger should be set to all booking engine \/ distributor events as described previously.

The Track Type of the event shouldn't be important in this case, you can even re-use the same tag as for tracking all booking engine \/ distributor events in analytics.
Be sure to also enable Enhanced Ecommerce in your Google Analytics, under **Admin &gt; Ecommerce** settings. The Enhanced Ecommerce plug-in should not be used alongside the Ecommerce plug-in for the same property.

![](../../.gitbook/assets/image.png)


## Troubleshooting

### There are no events or ecommerce transactions tracked after a redirect to the Mews Merchant page

You have probably included the container in your website, however, you haven’t set the container id in Distributor. Meaning that after the redirect, Distributor will not know anything about your container. You should set up your GTM container’s id in the Distributor's configuration in Mews Commander.

### I’ve set up the container correctly but there are still no events tracked

If you have everything set up correctly and you still cannot see events tracked, please, ensure that you’re not using any ad-blocking or similar software in your browser. They tend to block not only ads, but also tracking software like Google Tag Manager. Disabling the software for testing or adding your website to the exceptions should solve the issue.

> Important: If you are using Mews Payments, you need to disable the software for the \*.mews.com domain too.

### The Tag Assistant Chrome extension shows me a warning about multiple installations, but I use only one

Distributor includes our Mews Google Tag Manager container \(id`GTM-M7JV35D`\) to keep statistics in our own Google Analytics. We use that data for a global Distributor performance measuring, to have an idea about performance in hotels that don’t use Analytics and for the ability to build our own statistics on top of the Analytics API in Commander.

Having multiple installations is perfectly fine, if you keep a common data layer name for all of them, which we do. Please, see the official documentation: [https://developers.google.com/tag-manager/devguide\#multiple-containers](https://developers.google.com/tag-manager/devguide#multiple-containers)

| Next |
| :-- |
| [Google Triggers Reference](google-triggers-reference.md) |
