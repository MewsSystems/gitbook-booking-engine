# How to migrate booking engine off mews.li

> ⚠️ Support for this outdated implementation was discontinued as of May 1 - we are not responsible for the functionality of the booking engine on this domain

## Standalone Booking Engine migration

Find every occurrence of links containing `https://mews.li` domain pointing to the standalone booking engine hosted on our domain and replace them with `https://app.mews.com`. See [Standalone implementation guide](../booking-engine-standalone/getting-started.md).

### Example

#### ❌ Deprecated implementation
```html
<a href="https://www.mews.li/distributor/6b87e134-8c75-468a-82d4-aca900c43c70">Book Now</a>
```
#### ✅ After migration implementation
```html
<a href="https://app.mews.com/distributor/6b87e134-8c75-468a-82d4-aca900c43c70">Book Now</a>
```
## Widget Booking Engine migration

Replace the domain in your booking engine loading script from `https://mews.li` to `https://api.mews.com`. See [installation guideline](../booking-engine-widget/getting-started.md).

#### ❌ Deprecated implementation
```html
<head>
    ...
    <script src="https://mews.li/distributor/distributor.min.js"></script>
    ...
</head>
```

#### ✅ After migration implementation
```html
<head>
    ...
    <script src="https://api.mews.com/distributor/distributor.min.js"></script>
    ...
</head>
```
After a successful migration, the keyword `mews.li` should no longer appear on your website.

If you have any questions, please contact us at support@mews.com.
