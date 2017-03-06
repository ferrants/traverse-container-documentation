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
| `email`     | Plaintext (non-hashed) email address. *The Container will normalize and hash the email address client-side, and it will not be transmitted*.<sup id="a1">[1](#f1)</sup> | Yes |
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
| `aaid`      | Android ID. | No |
| `gaid`      | Google's Advertising ID. | No |
| `idfa`      | Apple's iOS Identifier for Advertisers. | No  |
| `waid`      | Microsoft's Windows Advertising ID. | No |
| `uaid`      | Any unknown advertising ID. Use this value if you are uncertain which type you are receiving. | No |
| `uaidHash`  | Use this if you meet the criteria above, your ID has been hashed, and you do not know which algorithm was used. | No |

<sub><b id="f1">1</b> The Container automatically handles the normalization and hashing of potentially sensitive fields. You may set these hashes manually using the following the naming convention: {parameter name}{hash type}{original character casing}. E.g. `emailMd5Upper`, `waidSha1Lower`, etc. If you choose to do this, we require all three of Md5, Sha1, and Sha256 hashes for both upper and lower-case input values. [↩](#a1)</sub>

Example
-------

Load the container and initialize with some user data:

```
<script src="https://static.traversedlp.com/v1/container/traverse-container.js?clientId=YOUR-CLIENT-ID-HERE" type="text/javascript"></script>
<script type="text/javascript">
TraverseContainer.start({
  email:     "john.doe@example.com", /* The Container will normalize and hash the email address. */
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

Initializing with hashed email addresses:

```
TraverseContainer.start({
  emailMd5Lower:     "1105677c8d9decfa1e36a73ff5fb5531",
  emailMd5Upper:     "d0768523e91903f0b6254679f8ed4568",
  emailSha1Lower:    "ba9d46a037766855efca2730031bfc5db095c654",
  emailSha1Upper:    "ddbead35b161ee92ae864505d4a78bc6c09d327f",
  emailSha256Lower:  "39e630f520f207b15632b701131a8df516270f23111e8d7cd7a38b724974ca6c",
  emailSha256Upper:  "bc7132be2f18de68eb81016fea548dd654c1362759b6dc5b79a0786f6ec13711",
});
```


Best practices
--------------

1. The Container is asynchronous, so always load it from the *target* of a form submit, rather than *on* submit, or it will not have time to record the [data](#user-object) before the user navigates to the next page!
2. For best compatibility with your page, load the Container from the HTML `body` section rather than the `head`.
3. To avoid affecting page-load time, load the Container from the bottom of your HTML.
