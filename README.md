# Branch Web SDK

**[New documentation portal](https://dev.branch.io) and [support portal with user forums](http://support.branch.io)**.  This documentation outlines the functionality of the Branch Metrics Web SDK, and how to easily incorporate it into a web app.

Live demo: [https://cdn.branch.io/example.html](https://cdn.branch.io/example.html)

## Installation

### Requirements

This SDK requires only native browser Javascript and has been tested in all modern browsers with sessionStorage capability. No 3rd party libraries are needed to make use of the SDK as it is 100% native Javascript.

### Browser Specific Support

| Chrome | Firefox | Safari | IE |
|:--------:|:-------:|:--------:|:--------:|
| &#10004; |&#10004; | &#10004; | 9, 10, 11 |

#### Specific Browser Support Status

[![Sauce Test Status](https://saucelabs.com/browser-matrix/branchmetrics.svg)](https://saucelabs.com/u/branchmetrics)

### Branch Key (formerly App ID)

You will need to create a [Branch Metrics app](http://branch.io) to obtain your Branch Key (you will have the option to toggle between live and test modes).

### Quick Install (Web SDK)

#### Manual installation

_Be sure to replace `BRANCH KEY` with your actual Branch Key found in your [account dashboard](https://dashboard.branch.io/#/settings)._

**[Formerly App ID](CHANGELOG.md)** Note that for the time being, initializing the Web SDK with an App ID will still work, it is strongly recomended you switch to using your live and test Branch Keys.

```html
<script type="text/javascript">

	(function(b,r,a,n,c,h,_,s,d,k){if(!b[n]||!b[n]._q){for(;s<_.length;)c(h,_[s++]);d=r.createElement(a);d.async=1;d.src="https://cdn.branch.io/branch-v1.7.1.min.js";k=r.getElementsByTagName(a)[0];k.parentNode.insertBefore(d,k);b[n]=h}})(window,document,"script","branch",function(b,r){b[r]=function(){b._q.push([r,arguments])}},{_q:[],_v:1},"addListener applyCode banner closeBanner creditHistory credits data first getCode init link logout redeem referrals removeListener sendSMS setIdentity track validateCode".split(" "), 0);

	branch.init('BRANCH KEY', function(err, data) {
    	// callback to handle err or data
	});
</script>
```

#### Bower or npm installation

If you use Bower or npm, you can run `bower install branch-sdk` or `npm install branch-sdk` respectively to get the SDK.

#### Common.JS and RequireJS compatibility

In addition to working as a standalone library, the Branch SDK works great in CommonJS environments (browserify, webpack) as well as RequireJS environments (RequireJS/AMD). Just `require('branch')` or `define(['branch'], function(branch) { ... });` to get started!

#### Initialization and Event Handling

You should initialize the Branch SDK session once the 'deviceready' event fires and each time the 'resume' event fires.  See the example code below. You will need your Branch Key from the Branch dashboard.

```js
  branch.init("YOUR BRANCH KEY HERE", function(err, data) {
  	app.initComplete(err, data);
  });
```

The session close will be sent automatically on any 'pause' event.

### SDK Method Queue

Initializing the SDK is an asynchronous method with a callback, so it may seem as though you would need to place any method calls that will execute immediately inside the `branch.init()` callback. We've made it even easier than that, by building in a queue to the SDK! The only thing that is required is that `branch.init()` is called prior to any other methods. All SDK methods called are guaranteed to: 1. be executed in the order that they were called, and 2. wait to execute until the previous SDK method finishes. Therefore, it is 100% allowable to do something like:

```js
branch.init(...);
branch.banner(...);
```

If `branch.init()` fails, all subsequent branch methods will fail.

## API Reference

# Branch Metrics Web SDK

This README outlines the functionality of the Branch Metrics Web SDK, and how to easily incorporate it into a
[Web](https://github.com/BranchMetrics/Web-SDK/blob/master/WEB_GUIDE.md#linkdata-callback)
or [Cordova/PhoneGap](https://github.com/BranchMetrics/Cordova-Ionic-PhoneGap-Deferred-Deep-Linking-SDK/blob/master/README.md#linkdata-callback) app.

Live demo of a web based implementation: [https://cdn.branch.io/example.html](https://cdn.branch.io/example.html)

## Overview

The Branch Web SDK provides an easy way to interact with the Branch API on your website, web app, or PhoneGap/Cordova mobile app. It requires no frameworks, is 100% native JavaScript and is only ~9K gzipped.

To use the Web SDK, you'll need to first initialize it with your Branch Key found in your [Branch dashboard](https://dashboard.branch.io/#/settings). You'll also need to register when your users login with `setIdentity`, and when they logout with `logout`.

Once initialized, the Branch Web SDK allows you to create and share links with a banner (web only), over SMS, or your own methods by generating deep links. It also offers event tracking, access to referrals, and management of credits.

## Register Your App

Getting started with either a Web or Cordova integration is simple, and begins with obtaining a Branch Key. You can sign up for your own Branch Key at [https://dashboard.branch.io](https://dashboard.branch.io)

## Web Based Integration

### [Full Documentation for the Web SDK](https://github.com/BranchMetrics/Web-SDK/blob/master/WEB_GUIDE.md)

Adding the Branch Web SDK source code to your project can be done manually, or by using Bower or npm: `bower install branch-sdk` or `npm install branch-sdk` respectively.

__Be sure to replace `BRANCH KEY` with your actual Branch Key found in your [account dashboard](https://dashboard.branch.io/#/settings).__

**[Formerly App ID](https://github.com/BranchMetrics/Web-SDK/blob/master/CHANGELOG.md)** Note that for the time being, initializing the Web SDK with an App ID will still work, it is strongly recomended you switch to using your live and test Branch Keys.

```html
<script type="text/javascript">

	(function(b,r,a,n,c,h,_,s,d,k){if(!b[n]||!b[n]._q){for(;s<_.length;)c(h,_[s++]);d=r.createElement(a);d.async=1;d.src="https://cdn.branch.io/branch-v1.7.1.min.js";k=r.getElementsByTagName(a)[0];k.parentNode.insertBefore(d,k);b[n]=h}})(window,document,"script","branch",function(b,r){b[r]=function(){b._q.push([r,arguments])}},{_q:[],_v:1},"addListener applyCode banner closeBanner creditHistory credits data first getCode init link logout redeem referrals removeListener sendSMS setIdentity track validateCode".split(" "), 0);

	branch.init('BRANCH KEY', function(err, data) {
    	// callback to handle err or data
	});
</script>
```

## Cordova/PhoneGap

### [Full Documentation for the Cordova Web SDK](https://dev.branch.io/recipes/quickstart_guide/cordova/#installing-the-sdk-files)

The Web SDK is provided as a plugin for Cordova and can be installed with Cordova plugin or the Plugman tool.  Point the tool at this repositry, https://github.com/BranchMetrics/Cordova-Ionic-PhoneGap-Deferred-Deep-Linking-SDK.  For example:

```sh
$ cordova plugin add https://github.com/BranchMetrics/Cordova-Ionic-PhoneGap-Deferred-Deep-Linking-SDK
```

You should initialize the Branch SDK session once the 'deviceready' event fires and each time the 'resume' event fires.  See the example code below. You will need your Branch Key from the Branch dashboard.

```js
  branch.init("YOUR BRANCH KEY HERE", function(err, data) {
  	app.initComplete(err, data);
  });
```

## Appcelerator Titanum

### [Full Documentation for the Titanium Web SDK](https://dev.branch.io/recipes/quickstart_guide/titanium/)

The Web SDK is provided as a module for Titanium.

You should initialize the Branch SDK session once the 'deviceready' event fires and each time the 'resume' event fires.  See the example code below. You will need your Branch Key from the Branch dashboard.

```js
  branch.init("YOUR BRANCH KEY HERE", function(err, data) {
  	app.initComplete(err, data);
  });
```

## Commonly Used Features

#### App Smart Banner
While only available for websites and web apps (not Cordova), the app smart banner is one of the most widely used features of the Web SDK. A few short lines of code will produce an automatically
generated, highly customizeable banner at either the top or bottom of the page it is installed on. The banner automatically styles itself for Android, iOS, and desktop, and generates a mobile deep
link if on a mobile deive, or displays a "TXT me the app form" if on desktop. If you are looking for a very simple way of getting deeplinking setup on your website - both desktop and mobile - the
Smart banner is a great start!

Get Started Installing the App Smart Banner for Web [Here](https://github.com/BranchMetrics/Web-SDK/blob/master/WEB_GUIDE.md#smart-app-sharing-banner)

For an in-depth explanation of everything the App Smart Banner can do, see the [Smart Banner Guide](https://github.com/BranchMetrics/Web-SDK/blob/master/SMART_BANNER_GUIDE.md)!

| iOS Smart Banner | Android Smart Banner | Desktop Smart Banner |
|------------------|----------------------|----------------------|
| ![iOS Smart Banner](docs/images/ios-web-sdk-banner-1.0.0.png) | ![Android Smart Banner](docs/images/android-web-sdk-banner-1.0.0.png) | ![Desktop Smart Banner](docs/images/desktop-web-sdk-banner-1.0.0.png) |

#### Short link generation
Powerful, customizeable, and easy-to-create deeplinks are what Branch does best. The Web SDK delivers on this promise of providing a simple and powerful function for generating short deep links
asynchronously: `link()`. The method has all of the same options and parameters available on the public API `POST /v1/url` endpoint, and is called from a robust queueing mechanism and XHRRequest
implementation with JSONP fallback that is well tested down to IE9, and every major browser.

Get Started Generating Short Deep Links for [Web](https://github.com/BranchMetrics/Web-SDK/blob/master/WEB_GUIDE.md#linkdata-callback) or
[Cordova](https://github.com/BranchMetrics/Cordova-Ionic-PhoneGap-Deferred-Deep-Linking-SDK/blob/master/README.md#linkdata-callback)

## Using the Sample Web App

We provide a sample web app which demonstrates what Branch Metrics Web SDK can do. The online version can be found at <https://cdn.branch.io/example.html>. Alternatively, you can open `example.html` locally to for the same effect.

To modify this local web app, edit `src/web/example.template.html` first, and then run `make`, which will automatically update `example.html`. Refrain from manually editting `example.html`.

___

## Contributing
Whether you are an avid engineer, a partner, or a Branch employee, we activley welcome feature ideas and pull requests! Prior to actually writing code for a feature, it is best to reach out to us first, as we may already have something in the pipeline.

To build the Web SDK, you'll need to run `npm install` to grab the necessary packages, be sure you have [make](http://www.gnu.org/software/make/),
[python](https://www.python.org/downloads/) (comes with Mac OSX), [perl](http://learn.perl.org/installing/osx.html),
and the [Google Closure Compiler](https://developers.google.com/closure/compiler/) (Closure compiler is automatically installed when you run `make` the first time.)

For an in-depth guide to working with developing for the Web SDK, refer to the [release documentation](https://github.com/BranchMetrics/Web-SDK/blob/master/RELEASE_DOCUMENTATION.md).

___

## Bugs / Help / Support

Feel free to report any bugs you might encounter in the repo's issues. Any support inquiries outside of bugs
please send to [support@branch.io](mailto:support@branch.io).

