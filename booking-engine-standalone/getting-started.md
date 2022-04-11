# Getting started

The URL of the Booking Engine Standalone page has the following format:

```text
https://api.mews.com/distributor/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee
```

The `aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee` part should be replaced with your Booking Engine configuration id.
See [Where to get configuration id](../faq.md#where-to-get-configuration-id) for details of where to find it.

> Note:️ Make sure you are using Booking Engine configuration id, not enterprise id or other id.

## Multi-enterprise Booking Engine

If you want to use a Booking Engine with multiple enterprises, you can place several Booking Engine configurations ids together, separated by a semicolon \(the theme will be pulled from the id of the first configuration in the URL\).

```text
https://api.mews.com/distributor/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee;ffffffff-gggg-hhhh-iiii-jjjjjjjjjjjj
```

## Customization

You can use [Deeplinks](deeplinks.md) to customize Booking Engine Standalone behavior. 
