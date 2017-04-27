---
title: "Changelog"
weight: 30
---

This page lists the breaking changes that came with each API version change. API clients must send a
header called `X-CM-MaxVersionSupported` with an integer value, indicating what version your client
supports.

This page doesn't list non-breaking changes, such as fields or endpoints being added.

New API clients must be built using the latest API version.

## `X-CM-MaxVersionSupported: 2`

`/offer/search-hints` response has changed from arrays of strings to arrays of objects - each object
has a name string and ID string.

## `X-CM-MaxVersionSupported: 3`

The field `offerInfo` in offer objects has been renamed to `occurrences`.

## `X-CM-MaxVersionSupported: 4`

The fields `geoPosition` and `gpsCoordinates` (they were the same) in restaurants objects have been renamed/combined into `geoPoint`.

## `X-CM-MaxVersionSupported: 5`

Each offer occurrence can now have a different start and end time, compared to the parent offer.

Each offer occurrence, within the object `offer.occurrences`, may now have a `startTime` and
`endTime` field. If either of these are null, assume the parent offer's start or end time.

The fields `voucher.startTime` and `voucher.endTime` should now be used when displaying a voucher's
start and end time, instead of `offer.startTime` and `offer.endTime`.

After a voucher has been reserved, it's time range can be expanded, not reduced, so existing
clients will continue to work with API v4 and below, but the voucher times will not always be
correct.

## `X-CM-MaxVersionSupported: 6`

The offer fields `isActive`, `isRemoved`, and `isSuspended` have been merged into a single field
called `status`. The valid status values are `INACTIVE_BY_DEFAULT`, `ACTIVE_BY_DEFAULT`, `SUSPENDED`
and `DELETED`.

The restaurant fields `isAuthorised` and `isDeleted` have been merged into a single field called
`status`. The valid status values are `UNAUTHORISED`, `AUTHORISED` and `DELETED`.

## `X-CM-MaxVersionSupported: 7`

Each offer now has a field `areGoldBonusesExcluded`. If this is true, gold bonuses (a.k.a. MunchCoins)
cannot be used when reserving a voucher for the offer.

Each offer now has a field `maximumCoversPerVoucher`. If this is non-null, voucher reservations may
not be reserved with more than this number of covers.

The offer field `lastDate` has been renamed to `endDate` to be consistent with other parts of the API.

## `X-CM-MaxVersionSupported: 8`

This is a big release, with completely new voucher types!

The endpoint `GET /users/search/referral-code/{code}` has been deprecated and moved to
`GET /referral-codes/{code}`. The old endpoint will continue to check consumer referral codes only,
while the new endpoint will check consumer referral codes and new types like blogger codes,
restaurant-specific codes and marketing codes.

The consumer registration endpoints now accept other types of referral codes (see above) in API v8.
API v7 and below will continue to only accept consumer referral codes.

Vouchers can now have different "types":

* `PERCENT_OFF_ANY_FOOD_ON_DATE` - a traditional CityMunch voucher, with a `date`, `startTime`,
    `endTime`, `offer` and `totalDiscount`.

* `PERPETUAL_PERCENT_OFF_SPECIFIC_ITEM` - for example "20% off coffee until 31st December" - has the
    new fields `itemName` and `expiresOnDate`, keeps the traditional field `totalDiscount`, but
    does not have the traditional fields `date`, `offer`, `startTime` or `endTime`.

* `PERPETUAL_SPECIFIC_ITEM_FOR_FREE` - for example "free coffee until 31st December" - has the new
    fields `itemName` and `expiresOnDate`, but does not have the traditional fields `date`, `offer`,
    `startTime`, `endTime` or `totalDiscount`.

* `PERPETUAL_N_FOR_1` - for example "2 for 1 on any curry" - has the new fields `nFor1`, `itemName`
    and `expiresOnDate`, but does not have the traditional fields `date`, `offer`, `startTime`,
    `endTime` or `totalDiscount`.

In API v7 and below, only vouchers with type `PERCENT_OFF_ANY_FOOD_ON_DATE` will be visible.

The endpoint `/vouchers/search/own-active-or-recently-active` has been removed entirely.

The endpoint `/vouchers/search/own-first-voucher` has been removed entirely.

## `X-CM-MaxVersionSupported: 9`

The structure of the endpoint `/restaurants/search/authorised-restaurants` has changed under
the `allActiveOffers` key.

## `X-CM-MaxVersionSupported: 10`

The restaurant field `cuisineType` field has been renamed to `primaryTag`, and a *new* `cuisineType`
field has been added. A `businessType` field has also been added.

In versions 9 and below, the restaurant's "primary tag" will continue to serialize as `cuisineType`.

## `X-CM-MaxVersionSupported: 11`

The voucher field `seatsReserved` field has been renamed to `coversReserved`.

<!-- When documenting a new version, remember to update the latest version number in `documentation.md`. -->
