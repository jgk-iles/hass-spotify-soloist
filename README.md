# Spotify Soloist for Home Assistant

A Home Assistant add-on that turns your Home Assistant device into a
**lossless** Spotify Connect speaker. It uses
[Spotify Soloist][soloist], Spotify's official headless Linux client.

It's a Soloist-based take on the
[Spotify Connect add-on][spotify-connect], which uses the unofficial
librespot library.

## Installation

[![Add repository to my Home Assistant][repo-badge]][repo-add]

Or add `https://github.com/jgk-iles/hass-spotify-soloist` under
**Settings** → **Add-ons** → **Add-on store** → ⋮ → **Repositories**,
then install **Spotify Soloist**.

You need a Spotify Premium account and your own Soloist API key. See the
[add-on documentation](soloist/DOCS.md).

## Add-ons

### [Spotify Soloist](soloist)

Lossless Spotify Connect speaker powered by Spotify Soloist.

## Note on Soloist distribution

Spotify does not allow Soloist binaries to be redistributed. This repository
and the add-on image contain none of Spotify's software. The add-on downloads
the official build directly from Spotify when it runs.

This project is not affiliated with Spotify.

[repo-add]: https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fjgk-iles%2Fhass-spotify-soloist
[repo-badge]: https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg
[soloist]: https://developer.spotify.com/documentation/soloist
[spotify-connect]: https://github.com/hassio-addons/app-spotify-connect
