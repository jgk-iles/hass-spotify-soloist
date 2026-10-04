# Changelog

## 0.1.1

- With the log level set to `debug`, the add-on now also logs the state of
  its audio streams and outputs on Home Assistant's audio server whenever it
  changes. This helps diagnose silence after a song changes.

## 0.1.0

- Initial release: Spotify Connect speaker powered by the official Spotify
  Soloist client, which supports lossless streams.
- Soloist is downloaded from Spotify at runtime (never bundled) and kept
  updated before its 90-day expiry.
- Optional network exposure of the Soloist WebSocket API.
