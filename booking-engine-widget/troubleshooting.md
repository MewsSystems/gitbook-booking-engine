# Troubleshooting

## Booking Engine shows an error "api.mews.com refused to connect"

### The fault

The browser says it can't open the page because of security, or there's a console error mentioning `api.mews.com` and `X-Frame-Options`.
For example:

![api.mews.com refused error Google Chrome](../.gitbook/assets/api-mews-com-refused-connect-chrome.png)
![api.mews.com refused error Mozilla Firefox](../.gitbook/assets/api-mews-com-refused-connect-firefox.png)

- `[Error] Refused to display 'https://api.mews.com/distributor' in a frame because it set 'X-Frame-Options' to 'sameorigin'.`
- `The loading of "https://api.mews.com/distributor" in a frame is denied by "X-Frame-Options" directive set to "sameorigin".`

### Explanation

The Booking Engine is not working because it is not installed correctly on your page.
Installing the Booking Engine in any other way than as described in this Guide is not supported and can cause errors such as "api.mews.com refused to connect".

You can try to confirm the Booking Engine is not installed correctly by inspecting the DOM of the page, as follows:

- Open the page with the Booking Engine and make it show the error.
- Open your browser developer tools with DOM/elements inspector.
- In the inspector, look for any tags like `<iframe src="https://api.mews.com/distributor/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee">`.

There shouldn't be any iframe tag with a `src` attribute pointing to `api.mews.com` domain.
If you find something like that, the problem could be in the way the Booking Engine is installed. And even if you didn't find anything like that, it's better to check if the Booking Engine is installed correctly.

### How to fix it

* Decide if you want to use Booking Engine Standalone or Booking Engine Widget (see [Ways to integrate](../FAQ/ways-to-integrate.md))

* Go through the relevant installation guide and make sure your page and code is doing everything correctly:
	* [Booking Engine Standalone Getting started guide](../booking-engine-standalone/getting-started.md)
	* [Booking Engine Widget Getting started guide](getting-started.md)

If you are using the Booking Engine Widget, pay special attention to the [Requirements](getting-started.md#requirements) section of the Booking Engine Widget Getting started guide, it has a list of things to do and a list of common mistakes that can occur during installation.
