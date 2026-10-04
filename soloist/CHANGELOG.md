# Changelog

## 0.2.0

- Soloist now plays through a PipeWire server inside the add-on, which
  forwards the audio to Home Assistant's audio system. PipeWire is Soloist's
  main audio output. The direct PulseAudio output it used before leaves the
  next song silent after a song ends on its own, even though the progress bar
  keeps moving.
- New `audio_backend` option to go back to the direct PulseAudio output
  (`pulseaudio`) if needed.
- Debug audio logging now covers both Soloist's stream in PipeWire and Home
  Assistant's audio system.

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
