# How to migrate booking engine off mews.li

> ⚠️ Support for this deprecated implementation will end on May 1, which may cause your booking engine to stop working.

## Standalone Booking Engine links migration

Find every occurrence links containing `https://mews.li` domain pointing to standalone booking engine hosted on our domain and replace them with `https://app.mews.com`. See [Standalone implementation guide](../booking-engine-standalone/getting-started.md).

### Example

#### ❌ Deprecated implementation
```html
<a href=href="https://www.mews.li/distributor/6b87e134-8c75-468a-82d4-aca900c43c70">Book Now</a>
```
#### ✅ After migration implementation
```html
<a href=href="https://app.mews.com/distributor/6b87e134-8c75-468a-82d4-aca900c43c70">Book Now</a>
```
## Widget Booking Engine migration

Replace domain in your booking engine loading script from `https://mews.li` to `https://api.mews.com`. See [installation guideline](../booking-engine-widget/getting-started.md).

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
After a successful migration, the keyword `mews.li` should not appear on your website anymore.

If you have any questions, please contact us at support@mews.com.
