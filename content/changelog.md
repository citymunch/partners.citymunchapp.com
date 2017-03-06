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
