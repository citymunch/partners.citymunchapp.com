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
