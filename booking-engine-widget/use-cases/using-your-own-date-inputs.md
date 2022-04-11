# Using your own Date inputs

This guide will show you how to have a form with date inputs which will open Distributor with given dates after users submit it.


## Prerequisites

{% hint style="info" %}
Make sure you fulfill all the required [prerequisites](./prerequisites.md). Without doing so the code can be hard to understand or the behavior of the code can differ.
{% endhint %}

## Code

Comments with numbers have more details below the code. [This guide is written for production environment](./use-own-date-inputs.md#4.-this-guide-is-written-for-production-environment)

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8" />
        <!-- 1. Install Distributor loader script as close to the opening <head/> tag as possible -->
        <script src="https://api.mews.com/distributor/distributor.min.js"></script>
        <title>My page</title>
    </head>
    <body>
        <!-- 2. Add form with date inputs. -->
        <form id="date-form">
            <label for="start">Start date:</label>
            <input type="date" id="start" name="start" required />
            <label for="end">End date:</label>
            <input type="date" id="end" name="end" required />
            <input type="submit" id="dates-submit" value="Loading..." disabled />
        </form>

        <script>
            // 3. Initialize Distributor Widget just before the closing </body> tag.
            Mews.Distributor(
                // 3.1 Set configuration id of your Distributor.
                {
                    configurationIds: ['Your Distributor configuration id'],
                },
                // Add callback which will enable Submit button and open Distributor Widget upon button click.
                function (api) {
                    // Listen on submit and when users submit, open Distributor with given dates.
                    const listenOnSubmit = () => {
                        // Find the form in DOM and listen on submit.
                        const form = document.getElementById('date-form');

                        form.addEventListener('submit', event => {
                            // Don't use the default submit button behavior. We want to handle it ourselves.
                            event.preventDefault();
                            // Get the dates from the date form.
                            const { start, end } = event.target.elements;
                            const [startYears, startMonths, startDays] = start.value.split('-');
                            const [endYears, endMonths, endDays] = end.value.split('-');

                            const startDate = new Date(startYears, startMonths - 1, startDays);
                            const endDate = new Date(endYears, endMonths - 1, endDays);
                            // Use Distributor Widget API to set the dates in Distributor Widget and open it.
                            api.setStartDate(startDate);
                            api.setEndDate(endDate);
                            api.open();
                        });
                    };

                    listenOnSubmit();

                    // Enable the submit button, because Distributor Widget is ready to be used.
                    const enableSubmit = () => {
                        const submitButton = document.getElementById('dates-submit');
                        submitButton.value = 'Submit';
                        submitButton.disabled = false;
                    };
                    enableSubmit();
                }
                // 4. This guide is written for production environment.
            );
        </script>
    </body>
</html>
```

### 1. Install Distributor loader script

For more details see [getting started section for installing Distributor loader script](../getting-started.md#install-distributor-loader-script).

### 2. Add form with date inputs

We've added just a simple form with date inputs as an example to give you an idea how to connect your own HTML elements. On your own page you can use any date inputs you want, you just need to connect them with Distributor Widget. Similarly, as later code shows.

The submit button in the form is disabled at page load, so users can't submit the form before the form and Distributor Widget are ready to be used. We enable it later when they're ready.

### 3. Initialize Distributor Widget

#### 3.1 Set configuration id of your Distributor

If you are not sure where to find the configuration id, see [where to get configuration id](../../faq.md#where-to-get-configuration-id) for details.

### 4. This guide is written for production environment

If you want to test this code in different environment, please refer to our guide for [testing in demo/staging/testing environment](./testing-in-staging-environment.md).

## Conclusion

In this article, you've learned how to add a simple form with date inputs to your page and connect its submit button to Distributor Widget. So when users select the dates and submit the form, Distributor Widget will open with given dates selected.

Distributor Widget API supports more than setting dates and opening it. See the other [Distributor Widget API options](../reference.md) to find other options you could use. You can also check out some [other use cases](./README.md).
