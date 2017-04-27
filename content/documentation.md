---
title: "Documentation"
weight: 20
---

## Environments

We have two public environments: production (typically shortened to 'prod') and UAT (user acceptance
testing, i.e. a test environment).

The prod environment must only be used for real-world users, and must not be used for testing.

The UAT environment may be used for testing. This environment does not affect real restaurants, for
example if a user reserves a voucher on UAT, the restaurant will not be notified by email or charged
for the voucher.

The environments are separated by host: `prod-api.citymunchapp.com` and `uat-api.citymunchapp.com`.

The data in the UAT environment **may** be replaced with a copy of the production database on an
infrequent basis, for example to make sure the restaurants on UAT aren't too different to prod.

## API Swagger docs

Our API endpoints and models are documented with [Swagger](http://swagger.io/).

Our production Swagger page is at [prod-api.citymunchapp.com/swagger-ui.html](https://prod-api.citymunchapp.com/swagger-ui.html)

The UAT (test environment) Swagger page is at [uat-api.citymunchapp.com/swagger-ui.html](https://uat-api.citymunchapp.com/swagger-ui.html)

From there, you can view every endpoint, the request format and the response format.
For example, if you click on "Authentication" and then click `POST /authentication/login`, you will
see that to login as a user, you would send a JSON request with the keys `email` and `password`,
and get a response with the keys `isLoggedIn`, `user` and `authenticationToken`.

You can also use [this JSON file](https://prod-api.citymunchapp.com/v2/api-docs?group=com.citymunch)
to auto-generate code in your favourite language, using a tool like
[Swagger Code Generator](https://github.com/swagger-api/swagger-codegen)

## Terminology

**User**: a person who has an involvment with CityMunch. Each user has a **role**, which describes
what type of user they are. The role may be **CONSUMER** (a user who can reserve and redeem vouchers)
or **MERCHANT** (a user who works for a restaurant).

**Restaurant**: A food place, which could be a restaurant, cafe, deli, street van, or other type of
establishment.

**Offer**: A percent-off-the-food-bill offering from a restaurant, for example
"20% off at restaurant X between 1pm and 3pm" is an offer.

**Offer occurrence**: An offer on a specific day. For example if an offer repeats on Mondays,
Tuesdays and Fridays, then an occurrence would be 5 December 2016, as would 6 January 2017. An
occurrence of an offer can have different details, e.g. a higher discount (for example if it starts
raining on the occurrence date) or a lower discount (for example if the restaurant suddenly
gets busy on the occurrence date).

**Voucher**: When a user has decided they want to take advantage of an offer, they reserve a voucher.

**Gold bonus**: Allows a user to boost their voucher discounts by an extra 5%. Branded within
CityMunch as "MunchCoins".

## HTTP headers

### Requests

All requests must have a `X-CM-MaxVersionSupported` header, which indicates what version of the API
your client supports. See the [changelog]({{< relref "getting-started.md" >}}). The newest API
version is **11**, so new clients should start with `X-CM-MaxVersionSupported: 11`.

Non-partner developers may simply call the API without identifying their client.

Partner developers must should an `Authorization` header with the value
`Authorization: Partner [API_KEY]`. Your API key can be retrieved from your partner portal. If your
API key becomes compromised, you must notify us immediately so we can blacklist it.

After a user has logged in via your client, you will be given the a user ID and authentication token
that uniquely identify the user. Send the headers `X-CM-UserId: (USER_ID)` and
`X-CM-AuthToken: (AUTH_TOKEN)` with all requests after the user has logged in.

### Responses

The API *may* respond with the header `X-CM-Logout: true` which indicates the logged in user is no
longer logged in, which may happen if, for example, they deactivate their account.

## Support

For technical support, email [partners@citymunchapp.com](mailto:partners@citymunchapp.com).
