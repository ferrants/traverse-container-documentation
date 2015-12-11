Documentation v1.0:
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
| `email`     | Plaintext (non-hashed) email address. This is the only required field. This plugin handles all normalization and hashing. | Yes |
| `first`     | First name | No |
| `last`      | Last name | No |
| `phone`     | Free-form phone number | No |
| `street1`    | The first line of the street address (e.g., `"123 Main St."`) | No |
| `street2`   | Second line of the stree address (e.g., `"Apartment 1A"`)        | No |
| `city`      | The city name  | No |
| `state`     | The full U.S. state name or two-letter abbreviation | No |
| `zip`       | The U.S. zip code, 5 or 9 letters, with or without hyphen | No |
| `audiences` | Array of audiences to which the user belongs. | No |
| `userId`    | Client-specific user identifier. | No |

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
  audiences: ["in-market car", "smoker"],
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
   audiences: ["in-market car", "smoker"],
   userId:    "123abc"
 });

</script>
```

Best Practices
--------------

This module should always be loaded in the page body rather than head. For optimal page load, place script tag at the bottom of your page HTML.
