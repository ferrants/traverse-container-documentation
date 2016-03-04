Traverse Container Documentation v1.2:
--------------------------------------

Contents
--------

  * [Overview](#overview)
  * [Resource URL](#resource-url)
  * [`User` object](#user-object)
  * [`Start` method](#start-method)
  * [Example](#example)
  * [Best practices](#best-practices)

Overview
--------

To use the Traverse Container, load it from the [resource URL](resource-url) and then call the [`start` method](#start-method).

Please see the [example](#example) and [best practices](#best-practices), below.

Resource URL
------------

The Container is hosted at the following URL:

<a href="">http(s)://static.traversedlp.com/v1/container/traverse-container.js?clientId=`clientId`</a>

| Parameter    | Description | Required |
| ------------ |------------ | -------- |
| `clientId` | Your 36-character client ID (includes hyphens). | Yes |

`Start` method
--------------

Initialize the Container by passing a [`user` object](#user-object) to the `start` method.

| Parameter    | Description | Required |
| ------------ |------------ | -------- |
| `user` | A [user](#user) object | Yes |

`User` object
-------------

A `user` object is written as a [Javascript Object Literal](http://www.dyn-web.com/tutorials/object-literal/) and may contain any of the following fields:

| Parameter   | Description | Required |
| ----------- | ----------- | -------- |
| `email`     | Plaintext (non-hashed) email address. The Container handles all normalization and hashing.<sup id="a1">[1](#f1)</sup> | Yes |
| `first`     | First name. | No |
| `last`      | Last name. | No |
| `phone`     | Free-form telephone number. | No |
| `carrier`   | Telephone carrier. | No |
| `street1`   | The first line of the street address (e.g., `"123 Main St."`). | No |
| `street2`   | Second line of the street address (e.g., `"Apartment 1A"`).        | No |
| `city`      | The city name.  | No |
| `state`     | The full U.S. state name or two-letter abbreviation. | No |
| `zip`       | The U.S. zip code, 5 or 9 numbers, with or without hyphen. | No |
| `context`   | Array of strings detailing the context of a user's interaction on the site, such as interests and actions. E.g. `['in-market car', 'smoker']`. | No |
| `gender`    | Gender of user, either `male` or `female`. | No |
| `birthYear` | Four-digit year in which the use was born (YYYY). | No |
| `birthMonth` | Numeric month in which the user was born (MM). | No |
| `birthDay`  | Day of the month in which the user was born (DD). | No |
| `userId`    | Client-specific string that uniquely identifies a user within your system. This could be a session ID, a visitor ID from a first-party cookie, or an ID passed via URL parameter from page to page. | No |
| `aaid`      | Android ID.<sup id="a1">[1](#f1)</sup> | No |
| `gaid`      | Google's Advertising ID.<sup id="a1">[1](#f1)</sup> | No |
| `idfa`      | Apple's iOS Identifier for Advertisers.<sup id="a1">[1](#f1)</sup> | No  |
| `waid`      | Microsoft's Windows Advertising ID.<sup id="a1">[1](#f1)</sup> | No |
| `uaid`      | Any unknown advertising ID. Use this value if you are uncertain which type you are receiving.<sup id="a1">[1](#f1)</sup> | No |
| `uaidHash`  | Use this if you meet the criteria above, your ID has been hashed, and you do not know which algorithm was used. | No |

<sub><b id="f1">1</b> The Container automatically handles the normalization and hashing of potentially sensitive fields. You may set these hashes manually using the following the naming convention: {parameter name}{hash type}{original character casing}. E.g. `emailMd5Upper`, `waidSha1Lower`, etc. If you choose to do this, we require both Md5 and Sha1 hashes for both upper and lower-case input values. [↩](#a1)</sub>

Example
-------

Load the container and initialize with some user data:

```
<script src="https://static.traversedlp.com/v1/container/traverse-container.js?clientId=YOUR-CLIENT-ID-HERE" type="text/javascript"></script>
<script type="text/javascript">
TraverseContainer.start({
  email:     "john.doe@example.com",
  first:     "John",
  last:      "Doe",
  phone:     "123-456-6789",
  street1:   "123 Main St.",
  street2:   "Apartment 1A",
  city:      "Springfield",
  state:     "IL",
  zip:       "12345",
  context:   ["in-market car", "smoker"],
  userId:    "123abc"
});
</script>
```

Best practices
--------------

1. The Container is asynchronous, so always load it from the *target* of a form submit, rather than *on* submit, or it will not have time to record the [data](#user-object) before the user navigates to the next page!
2. For best compatibility with your page, load the Container from the HTML `body` section rather than the `head`.
3. To avoid affecting page-load time, load the Container from the bottom of your HTML.
