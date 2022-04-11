# Multiple enterprises and preselected locations

This guide will show you how to open the Booking Engine with multiple enterprises and set preselected city/location.

## Prerequisites

{% hint style="info" %}
Make sure you fulfill all the required [prerequisites](./prerequisites.md). Without doing so the code of the use cases can be hard to understand or the behavior of the code can differ.
{% endhint %}

## Code

Comments with numbers have more details below the code. [This guide is written for production environment](./use-multi-enterprise-set-preselected-location.md#4.-this-guide-is-written-for-production-environment).

Code uses an example scenario with 3 hotels, with 2 of them from the same London location:

* One in Paris.
* One in London.
* Another one in London.

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8" />
        <!-- 1. Install Booking Engine loader script as close to the opening <head/> tag as possible -->
        <script src="https://api.mews.com/distributor/distributor.min.js"></script>
        <title>My page</title>
    </head>
    <body>
        <!-- 2. Add buttons for opening Booking Engine with specific location preselected -->
        <button disabled type="button" id="london-button">Loading...</button>
        <button disabled type="button" id="paris-button">Loading...</button>

        <script>
            // 3. Initialize Booking Engine Widget just before the closing </body> tag.
            Mews.Distributor(
                // 3.1 Set configuration ids of your Booking Engine.
                {
                    configurationIds: [
                        'Configuration id of first London hotel',
                        'Configuration id of second London hotel.',
                        'Paris hotel configuration id',
                    ],
                },
                // Add callback which will make the buttons open Booking Engine Widget and set the city/location.
                function (api) {
                    const initializeButton = (buttonId, cityId, buttonText) => {
                        const buttonElement = document.getElementById(buttonId);

                        buttonElement.addEventListener('click', event => {
                            event.preventDefault();

                            // Use Booking Engine Widget API to set the city/location and open the Booking Engine Widget.
                            api.setCity(cityId);
                            api.open();
                        });

                        buttonElement.innerHTML = buttonText;
                        buttonElement.disabled = false;
                    };

                    // 3.2 Prepare the city ids.
                    const londonCityId = 'Your London city id';
                    const parisCityId = 'Your Paris city id';

                    initializeButton('london-button', londonCityId, 'London hotels');
                    initializeButton('paris-button', parisCityId, 'Paris hotel');
                }
                // 4. This guide is written for production environment.
            );
        </script>
    </body>
</html>
```

### 1. Install Booking Engine loader script

For more details see [getting started section for installing Booking Engine loader script](../getting-started.md#install-booking-engine-loader-script).

### 2. Add buttons for opening Booking Engine with specific city preselected

Buttons are disabled on page load, so users can't click the buttons until the Booking Engine Widget is ready to be used. We enable it later when it's ready.

### 3. Initialize Booking Engine Widget

#### 3.1 Set configuration ids of your Booking Engine

If you are not sure where to find the configuration ids, see [where to get configuration id](../../faq.md#where-to-get-configuration-id) for details.

#### 3.2 Prepare the city ids

Even though it's called location in the UI, the api needs a city id.

If you are not sure where to find the city id, see [where to get city id](../../faq.md#where-to-get-city-id) for details.

If you have several hotels from the same city/location, the city id is the same in all of them. So use the first one you'll find.

### 4. This guide is written for production environment

If you want to test this code in different environment, please refer to our guide for [testing in demo/staging/testing environment](./testing-in-staging-environment.md).

## Conclusion

In this article, you've learned how to use multi-enterprise Booking Engine and how to set the preselected city/location.

Booking Engine Widget API supports more than preselecting city/location and opening it. See the other [Booking Engine Widget API options](../reference.md) to find other options you could use. You can also check out some [other use cases](./README.md).
