# Home Assistant Add-on: Spotify Soloist

This add-on turns your Home Assistant device into a Spotify Connect speaker
using [Spotify Soloist][soloist], Spotify's official headless client for
Linux. Pick it in any Spotify app and the music plays through the audio
output of your Home Assistant device.

Unlike librespot-based add-ons, Soloist is built by Spotify. It supports
Spotify's lossless (FLAC) streams.

This add-on is not made by, endorsed by or affiliated with Spotify.

## How Soloist gets installed

Spotify does not allow Soloist to be redistributed, so this add-on does
**not** contain it. When the add-on starts for the first time, it downloads
the official build for your device's architecture from Spotify's servers and
stores it in the add-on's data folder.

Soloist builds **expire 90 days** after Spotify publishes them. The add-on
keeps you up to date:

- On every start it checks for a newer build.
- While running (with `auto_update` on), it checks every 12 hours. It
  downloads newer builds in the background and switches to them once nothing
  is playing.
- If a build expires anyway, the add-on fetches a new one and restarts
  Soloist.

Your Home Assistant device therefore needs internet access.

## Installation

1. Add this repository to your Home Assistant add-on store
   (**Settings** → **Add-ons** → **Add-on store** → ⋮ → **Repositories**).
1. Install the **Spotify Soloist** add-on.
1. Get your Soloist API key (see below) and enter it in the **Configuration**
   tab.
1. Select your audio output device in the **Audio** section and click
   **Save**.
1. Start the add-on and check the logs.
1. Open Spotify on a phone or computer on the same network and pick your
   device from the device list. The first time you do this, Soloist logs in
   with your account. The session is saved, so you only have to do this once.

### Getting a Soloist API key

1. Sign in to the [Spotify for Developers dashboard][dashboard] with a
   **Spotify Premium** account.
1. Open the **Soloist API Key** section and generate a key.
1. Paste the key into the `api_key` option.

The key is personal. Don't share it, and don't post it in logs or issues.
Everyone who uses Soloist has to generate their own.

By using Soloist you accept the [Spotify Terms and Conditions of Use][tos].

## Configuration

Example configuration:

```yaml
name: Living room
api_key: your-soloist-api-key
initial_volume: 50
cache_size: 500
auto_update: true
```

### Option: `name`

The name of your device (the Spotify Connect target), as shown in the
Spotify apps.

### Option: `api_key`

Your personal Spotify Soloist API key. Required.

### Option: `initial_volume`

Initial volume in % from 0-100. It applies when the add-on starts.

### Option: `cache_size`

Maximum size of Soloist's playback cache in MB, stored in the add-on's data
folder. Use `0` for unlimited, otherwise at least `100`. Default: `500`.

### Option: `auto_update`

When enabled (the default), newer Soloist builds are downloaded in the
background and applied when nothing is playing. When disabled, the add-on
only checks for a newer build when it starts, or when the running build
expires.

### Option: `audio_backend`

How Soloist's audio reaches Home Assistant:

- `pipewire` (default): Soloist plays to a small PipeWire server inside the
  add-on, which forwards the audio to Home Assistant's audio system. This is
  Soloist's main audio output, the one Spotify tests on Raspberry Pi OS.
- `pulseaudio`: Soloist plays to Home Assistant's audio system (PulseAudio)
  directly, using its fallback output. With this backend the next song can
  stay silent after a song ends on its own, even though the progress bar
  keeps moving.

### Option: `websocket_port`

Soloist has a [WebSocket API][websocket] for playback state and control.
The add-on always runs it locally inside the add-on. Set a port here to
expose it on your network, for example for your own automations or
integrations.

**Warning**: the WebSocket API has no authentication. Anyone on your
network who can reach the port can control playback.

### Option: `log_level`

Controls how much the add-on logs: `trace`, `debug`, `info`, `notice`,
`warning`, `error` or `fatal`. Setting it to `debug` or `trace` also turns on
Soloist's verbose logging. It also logs every change to the audio streams
and outputs, which helps when sound goes missing. These lines start with
`[audio`:

- `pipewire …` lines show Soloist's stream inside the add-on: its state,
  mute, volume and which output it is linked to.
- `ha-audio …` lines show Home Assistant's audio system: whether the
  add-on's stream is paused (`corked`), muted, its volume and format, and
  which output it plays to.

## Audio quality and lossless

Soloist has no quality setting of its own. The streaming quality follows
your Spotify account and the quality settings in your Spotify app.
Lossless needs a plan that includes it.

Audio is played through Home Assistant's audio system. Choose the output
device in the add-on's **Audio** settings. Inside the add-on, audio stays in
32-bit floating point at 44.1 kHz (the rate of Spotify's streams, including
lossless), so it is not resampled before it reaches Home Assistant.

## Re-pairing / switching accounts

The Spotify session is stored in the add-on's data folder. To log in with a
different account, select the device from that account's Spotify app. To
start from scratch, uninstall and reinstall the add-on. This deletes its data
folder, including the downloaded Soloist build.

## Known issues and limitations

- A Spotify Premium account is required, both to generate the API key and to
  play music.
- Soloist announces itself on the network with mDNS (UDP port 5353). If
  something else on the host has that port exclusively, the device may not
  show up in the Spotify apps, and Soloist does not log an error. Try
  `log_level: debug` to see more.
- The Spotify iOS app may report the stream as 16-bit/44.1 kHz even when
  24-bit lossless is playing.
- Only 64-bit devices (`aarch64`, `amd64`) are supported.

## Third-party software

Spotify Soloist is Spotify's proprietary software. Its open-source notices
are in [Spotify's third-party licenses][licenses]. A copy is saved next to
the downloaded build (`THIRD_PARTY_LICENSES.txt`).

## License

The add-on (not Soloist) is released under the MIT License, see
[LICENSE.md][license].

[dashboard]: https://developer.spotify.com/dashboard
[license]: https://github.com/jgk-iles/hass-spotify-soloist/blob/main/LICENSE.md
[licenses]: https://developer.spotify.com/third-party-licenses#soloist-third-party-licenses
[soloist]: https://developer.spotify.com/documentation/soloist
[tos]: https://www.spotify.com/legal/end-user-agreement/
[websocket]: https://developer.spotify.com/documentation/soloist/reference/websocket-api
