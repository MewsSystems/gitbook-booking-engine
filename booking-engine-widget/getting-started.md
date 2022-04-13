# Getting started

By using the Booking Engine Widget your users can book directly from your website.

At a high level, the steps to start using booking engine Widget are:

1. [Install Booking Engine loader script](#step-1-install-booking-engine-loader-script)
2. [Initialize Booking Engine Widget](#step-2-initialize-booking-engine-widget)
3. [Set up overlay opening](#step-3-set-up-overlay-opening)
4. [All done!](#step-4-all-done)

In addition, you also have the following options:

* [Use callback function to control Widget](#use-callback-function-to-control-widget)
* [Set up as multi-enterprise](#set-up-as-multi-enterprise)

> ### Security note
> In order to embed the booking engine into your webpage, your site must be securely served over HTTPS.
> Any booking engine widget that is implemented on an insecure HTTP site will be redirected to the [standalone booking engine](../booking-engine-standalone/README.md).


## Step 1: Install Booking Engine loader script

To use booking engine Widget, you need to install booking engine loader script with a code snippet provided in the [Installation](./getting-started.md#installation) section.

The script will asynchronously prepare global `Mews.booking engine` object which you're going to use in further steps to initialize booking engine Widget.

### Requirements

Use the code snippet as is and as described. Doing otherwise will cause unexpected problems and is not supported.

#### Code snippet
* Do not place the snippet anywhere else than in the `<head>`.
* Do not modify the snippet in any way and do not attach the `async` attribute.
* Do not use the snippet inside an iframe.
* Do not add the [booking engine standalone](../booking engine-standalone/README.md) URL (e.q. `https://api.mews.com/booking engine/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee`) to the iframe.

#### Bundles and cache
* Do not pack the contents of the script files that the code snippet references into your own JavaScript bundle.
* Do not use booking engine script cached by your server, use the one from this guide.

The script file size is kept as minimal as possible (approx 11 kB gzipped) to allow quick webpage initialization. Also, serving the script from our CDN servers ensures seamless releases of new features, bugfixes and improvements.

#### Content Security Policy
* If you have a Content Security Policy (CSP) setup on your website, you need to [enable the domains booking engine uses](./getting-started.md#content-security-policy-1).

### Installation

Place the following `<script>` code snippet as is in the `<head>` of your web page's HTML output, preferably as close to the opening `<head>` tag as possible.

```html
<script src="https://api.mews.com/booking engine/booking engine.min.js"></script>
```

❎ **Incorrect** - DO NOT DO THIS:
```html
<script src="https://www.your_domain.tld/wp-content/cache/min/1/booking engine/booking engine.min.js?ver=1628071961"></script>
<script async src="https://api.mews.com/booking engine/booking engine.min.js"></script>
<script src="https://apps.mews.com/booking engine/prerelease/production/3.924.4/booking engine.js"></script>
<iframe src="https://api.mews.com/booking engine/booking engine.min.js"></iframe>
<iframe src="https://api.mews.com/booking engine/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"></iframe>
```

✅ **Correct**:
```html
<script src="https://api.mews.com/booking engine/booking engine.min.js"></script>
```

> Warning: Please double-check that you've added the script as instructed and followed all the [requirements](./getting-started.md#requirements). If the script tag is not used correctly, it can cause unexpected problems even when it seems everything is working.

#### Content Security Policy

If you have a Content Security Policy (CSP) setup on your website, the following domains should be enabled for booking engine to function correctly.

```text
*.mews.com
https://pay.datatrans.com/upp/payment/js/secure-fields-1.0.0.js
```

The last, datatrans, URL is for [PCI Proxy](https://www.pci-proxy.com/) which is the secure, PCI-DSS complaint solution that is used by our Merchant to process payment cards.


## Step 2: Initialize Booking Engine Widget

After the website has loaded, and the booking engine loader script prepared the global `Mews.booking engine` object, you can initialize booking engine Widget by calling global `Mews.booking engine` with some arguments:

> Note: **Important:** Make sure you initialize booking engine Widget by calling `Mews.booking engine` **only after** the website is loaded, otherwise the initialization will fail or not complete fully. 
> The easiest way to achieve this is to place the initialization code inside a `script` tag just before the closing `</body>` tag. But you can use a different approach, if you want.

In the following snippet, **replace the placeholder** `Your booking engine configuration id` with a **real booking engine configuration id** from the correct [environment](../booking engine-api-v1/environments.md). Here's more info about [where to get the configuration id](../faq.md#where-to-get-configuration-id).

```html
<!-- booking engine's initialization call, it creates new instance of booking engine. Use your booking engine configuration id. -->
<script>
    Mews.booking engine({
        configurationIds: [
            'Your booking engine configuration id',
        ],
        openElements: '.booking engine-open',
    });
</script>
```

This call creates an isolated (iframe based) overlay on your website and loads booking engine into it.

> Warning: The overlay and booking engine is not visible by default. You're going to solve this in the next section.


## Step 3: Set up overlay opening

To display the booking engine overlay, you should bind its opening to some action (e.g. clicking on a button).

booking engine can set this binding automatically for you, if you provide the second option `openElements` to `Mews.booking engine` and prepare the HTML elements which will be binded. You can find more info about `openElements` in [Options reference](./reference.md#options-reference).

The binding is delegated, so the elements and selectors don't need to exist during load of the website, but you still need to add the HTML elements yourself.

Knowing that, you can for example add the following HTML button with class `booking engine-open` (the class name we've used in the initialization code in code snippet from the previous section), and it  will open the booking engine Widget overlay upon a click:

```html
<!-- Example of button for opening the booking engine when openElements is set to '.booking engine-open' -->
<button class="booking engine-open">Book Now</button>
```

It's just an example, the automatic binding can attach click event listener to any HTML element.

> Note: Closing of booking engine is provided in the overlay by default, no configuration needed from your side.


## Step 4: All done!

This is all you need for the basic setup of Mews booking engine. What you've done:

- On page with this setup, loader script will prepare `Mews.booking engine`.
- After the page loads, your code will call `Mews.booking engine`. This will initialize booking engine Widget, create (for now) hidden overlay and bind opening actions to selected HTML elements, like buttons.
- When users click these HTML elements, booking engine Widget overlay will open, and they can book through it.
- They can close it anytime and see your page again.


## Use callback function to control Widget

> This step is optional

If you want to have a more customized setup, or you want to call some API functions on a booking engine instance to control it, you can provide a callback function as the second argument to the initialization call. 

This callback is later called asynchronously with an argument - booking engine instance. By calling methods on this instance you can control booking engine.

Very common example of this is [using a custom start and end date selectors that are part of your website and then passing user’s selection to booking engine](./use-cases/use-own-date-inputs.md):

```html
<!-- Example of setting custom dates. Useful if you have i.e. own calendars on website. -->
<script>
    Mews.booking engine(
        {
            configurationIds: [
                'Your booking engine configuration id'
            ],
            openElements: '.booking engine-open',
        },
        function (api) {
            // you can call API functions on a booking engine instance here
            // set different start and end date
            api.setStartDate(new Date(2022, 1, 1));
            api.setEndDate(new Date(2022, 1, 3));
        }
    );
</script>
```

> Note: To see a list of all available API calls, please consult [Widget API reference](./reference.md#api-reference).


## Set up as multi-enterprise

> This step is optional

booking engine can run in two basic modes - for a single enterprise or for multiple. The mode is chosen automatically during initialization, based on the count of configuration ids you have provided in the options. Whenever two or more hotels are loaded, the booking engine will start in the multi-enterprise mode. That means that it will add one more step to the booking flow - hotel selection. To add more hotels, simply pass their configuration ids into the`configurationIds`array option (here's [how you can get the configuration ids](../faq.md#where-to-get-configuration-id)):

```html
<script>
    Mews.booking engine({
        configurationIds: [
            'First configuration id',
            'Second configuration id',
            // and more...
        ],
    });
</script>
```
