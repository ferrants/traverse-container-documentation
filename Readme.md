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

  The plugin is initialized with a [contact](#contact) object and exposes no other methods.

###Methods

####init

  Initializes the container on your page, loading 3rd party pixels.

#####Parameters:

  [contact](#contact) object

#####Example

  `OurCompanyName.init({contact});`

###Contact

  A contact is written as a [Javascript Object Literal](http://www.dyn-web.com/tutorials/object-literal/) and may contain any of the following fields:

  | Parameter   | Description | Optional |
  | ------------- | ------------- | --- |
  | `email`     | Plaintext (non-hashed) email address. This is the only required field. This plugin handles all normalization and hashing. | No |
  | `emailMd5`     | Expects a [properly preprocessed](#preprocessing-email-addresses) email address, hashed using the MD5 algorithm. If both emailMD5 and emailSHA1 are set, the `email` field may be left blank. | Yes |
  | `emailSha1`     |  | Yes |
  | `first`     | First name | Yes |
  | `last`      | Last name | Yes |
  | `phone`     | Free-form phone number | Yes |
  | `street1`    | The first line of the street address (e.g., `"123 Main St."`) | Yes |
  | `street2`   | Second line of the stree address (e.g., `"Apartment 1A"`)        | Yes |
  | `city`      | The city name  | Yes |
  | `state`     | The full U.S. state name or two-letter abbreviation | Yes |
  | `zip`       | The U.S. zip code, 5 or 9 letters, with or without hyphen | Yes |

  To set, pass a contact object to the init function:

  ```
  OurCompanyName.init({
    email:    "john.doe@domain.com",
    first:    "John",
    last:     "Doe",
    phone:    "123-456-6789",
    street1:   "123 Main St.",
    street2:  "Apartment 1A",
    city:     "Springfield",
    state:    "IL",
    zip:      "1234"
  });
  ```

####Preprocessing email addresses

Before passing a hashed email address to our service, it must first be converted to a standard format. You must:

  - Remove all whitespace
  - Convert all characters to lower case

Example
-------

  Include our tag, and initialize with your client data

  ```
  <script src="resourceURL" type="text/javascript"><script/>
  <script type="text/javascript">
  OurCompanyName.init({
       "email":"jdoe@domain.com",
       "first": "John",
       "last": "Doe",
       "state":"CO"
     });
  </script>
  ```
  
Resource URL
--------------
  http://static.traversedlp.com/container/v1/traverse-container.js


Best Practices
--------------

  This module should always be loaded in the page body rather than head. For optimal page load, place script tag at bottom of page HTML.
