# Provider rules

This document gives the rules for each provider. Obey these rules in the code.

## MusicBrainz

MusicBrainz applies rate limits per source IP, per User-Agent, and globally. The source is
<https://musicbrainz.org/doc/MusicBrainz_API/Rate_Limiting>.

- Per source IP, the limit is 1 request per second on average. Above this rate, the server declines all requests with HTTP 503.
- A User-Agent with contact information has no limit. All anonymous User-Agents share 50 requests per second.
- The global limit is 300 requests per second.

Send `reso/<version> ( <contact-url> )` as the User-Agent.

Do not start background enrichment at a fixed time of day. Spread the requests over time.

In a test, use a recorded response. In a live run, send a maximum of 1 request per second
to MusicBrainz.

## Wikipedia

The text of Wikipedia has the license CC BY-SA. On the artist page, show the source and
the license.

## Audius

The operator examined the API terms of Audius.

Download an Audius track only if the artist marked the track as downloadable.

## Radio

Do not record radio.

## Fingerprints

No T1 provider for fingerprints exists. First, match on the artist, the title, and the
duration. AcoustID (T2, free app key) is an option for a later step.
