# Vantiv Integrated Payments Android Pay Web demo using Node and Heroku

Site adapted from [https://rsolomakhin.github.io](https://rsolomakhin.github.io)

## Requirements
* A [Vantiv eProtect account](https://www.vantiv.com/get-started)
* A Gmail or Google account
* A [Heroku](https://www.heroku.com) account (no credit card needed)
* An Android device
  * Android Pay app (available on Play Store)
  * An Android Pay compatible credit card (card will not be charged)
  * Chrome for Android

## Setup
First [Enable Android Pay](https://androidpay.developers.google.com/signup) using a gmail or google account.

Next [Signup for Android Pay Web Beta](https://docs.google.com/forms/d/e/1FAIpQLSeRreF7gYqSALxe0jHue9OM9rb07SarvvV3GjylmZgt_aXjpA/viewform)
and make sure the Google Account you give is the same one you used when you enabled Android Pay.

Here's how to fill out some of the fields:

For **Google Account** give the same account as when you enabled Android Pay.

For **Site Origin(s)** enter the domain you will be hosting the Android Pay Web site. If using Heroku this will be
`<sitename>.herokuapp.com` (See the 'How to host for free using Heroku' section below for what the site name will be).

For **Integration Type** select 'Gateway Integration (recommended)'

Leave **Network Token Public Encryption Key** blank as you're not using the Network Token Integration.

## How to host for free using Heroku

### Sign up for [Heroku](https://www.heroku.com) (no credit card needed)

Sign up then install the [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli).

Next from a terminal run `heroku login` and login.

Next clone this project to your computer and in your terminal change directories to that folder.

In pr.js customize Merchant Name on line 17 (does not have to match what you signed up with above). On line 18, change Merchant Id
to the one you received from Google in response to signing up for the Android Pay Web Beta.

On line 24 change `vantiv:merchantPayPageId` to your Vantiv eProtect PayPageId.

Run `heroku create` to create a new Heroku app with a random name (that you can change later).

Next do `git push heroku master` to push the site to Heroku. You can now browse to the page at `https://<sitename>.herokuapp.com` by
running `heroku open`.

### Testing Locally

First install all prerequisites by running `npm install` from a terminal window.

Then run `npm start` to start a Node server then browse to `http://localhost:3000/`. You should be able to open the page, 
but when the Buy button is clicked the message `PaymentRequest API is not supported.` will appear because the only 
currently supported browser is Chrome for Android.

### Testing from Android

Before you can run through a test Android Pay Web demo transaction you must first download the Android Pay
app to your Android device and add a credit card.

After that open Chrome on your Android device and browse to `https://<sitename>.herokuapp.com` and tab the Buy button and and
Android Pay sheet should slide up and lead you through the a transaction. Afterwards the page should display 'Thank you!'
followed by a JSON response:

```json
{
  "methodName": "https://android.com/pay",
  "details": {
    "billingAddress": {
      "address1": "124 Main St",
      "address2": "",
      "address3": "",
      "address4": "",
      "address5": "",
      "administrativeArea": "OH",
      "companyName": "",
      "countryCode": "US",
      "locality": "Cincinatti",
      "name": "John Doe",
      "postalCode": "12345",
      "sortingCode": ""
    },
    "instrumentInfos": [
      {
        "instrumentType": "VISA",
        "instrumentDetails": "1234"
      }
    ],
    "paymentDescriptions": [
      "Visa  • • • • 1234"
    ],
    "paymentMethodToken": "4426087674792681234"
  },
  "shippingAddress": null,
  "shippingOption": null,
  "payerEmail": null,
  "payerPhone": null
}
```

## Android Pay Web Resources

* [Web Payments at W3C](https://www.w3.org/Payments/)
* [Consumer Website for Android Pay](http://www.android.com/pay/)
* [Android Pay In-App developers site](https://developers.google.com/android-pay/)
* [Android Pay branding guidelines site](https://android-pay-toolkit.withgoogle.com/)
* [Bringing Easy and Fast Checkout with Payment Request API](https://developers.google.com/web/updates/2016/07/payment-request?hl=en)
* [Android Pay in PaymentRequest API](https://developers.google.com/web/fundamentals/discovery-and-monetization/payment-request/android-pay)