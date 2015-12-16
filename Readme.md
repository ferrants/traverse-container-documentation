Documentation v1.2:
-------------------

Contents
--------

  * [API](#api)
  * [Resource URL](#resource-url)
  * [Example](#example)
  * [Best Practices](#best-practices)

API
---

The plugin is initialized with a [user](#user) object and exposes no other methods.

###Methods

####TraverseContainer.start()

Sets the user data to be used by the Traverse container and initializes it
on your page.

#####Parameters:

[user](#user) object

#####Example

`TraverseContainer.start(user);`

####User

A user is written as a [Javascript Object Literal](http://www.dyn-web.com/tutorials/object-literal/) and may contain any of the following fields:

| Parameter   | Description | Required |
| ----------- | ----------- | -------- |
| `email`     | Plaintext (non-hashed) email address. The container handles all normalization and hashing.<sup id="a1">[1](#f1)</sup> | Yes |
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
| `aaid`      | Google's Android Advertising ID.<sup id="a1">[1](#f1)</sup> | No |
| `idfa`      | Apple's iOS Identifier for Advertisers.<sup id="a1">[1](#f1)</sup> | No  |
| `waid`      | Microsoft's Windows Advertising ID.<sup id="a1">[1](#f1)</sup> | No |
| `uaid`      | Any unknown advertising ID. Use this value if you are uncertain which type you are receiving.<sup id="a1">[1](#f1)</sup> | No |
| `uaidHash`  | Use this if you meet the criteria above, your ID has been hashed, and you do not know which algorithm was used. | No |

<sub><b id="f1">1</b> Our container automatically handles the normalization and hashing of potentially sensitive fields. You may set these hashes manually using the following the naming convention: {parameter name}{hash type}{original character casing}. E.g. `emailMd5Upper`, `waidSha1Lower`, etc. If you choose to do this, we require both Md5 and Sha1 hashes for both upper and lower-case input values. [↩](#a1)</sub>


To set, pass a user object to the start function:

```
TraverseContainer.start({
  email:     "john.doe@domain.com",
  first:     "John",
  last:      "Doe",
  phone:     "123-456-6789",
  street1:   "123 Main St.",
  street2:   "Apartment 1A",
  city:      "Springfield",
  state:     "IL",
  zip:       "12345",
  context: ["in-market car", "smoker"],
  userId:    "123abc"
});
```

Resource URL
------------

The Traverse container script may be loaded from the following URL:

http(s)://static.traversedlp.com/v1/container/traverse-container.js?clientId={your client ID}

| Parameter    | Description | Required |
| ------------ |------------ | -------- |
| `clientId` | Your 36-character client ID (includes hyphens). | Yes |

Example
-------

Include our tag, and initialize with your user data:

```
<script src="resourceURL" type="text/javascript"></script>
<script type="text/javascript">
TraverseContainer.start({
   email: "jdoe@domain.com",
   first: "John",
   last: "Doe",
   state: "CO",
   context: ["in-market car", "smoker"],
   userId:    "123abc"
 });

</script>
```

Best Practices
--------------

This module should always be loaded in the page body rather than head. For optimal page load, place script tag at the bottom of your page HTML.
