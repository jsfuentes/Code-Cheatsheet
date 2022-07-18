# Spotify

https://developer.spotify.com/dashboard/applications

Does not allow you to get friend info, must give ids and then you can see if they follow those specific ids. 

## Songs API

Builtin API to get the top songs for the user

Elixir - https://github.com/jsncmgs1/spotify_ex

```elixir
        types = ["artists", "tracks"]
        ranges = ["short_term", "medium_term", "long_term"]

        all_results =
          Enum.map(types, fn type ->
            range_results =
              Enum.map(ranges, fn range ->
                url =
                  "https://api.spotify.com/v1/me/top/#{type}?time_range=#{range}&limit=#{limit}"

                %HTTPoison.Response{status_code: 200, body: rawBody} =
                  HTTPoison.get!(url, headers)

                body = Jason.decode!(rawBody)
                {range, body["items"]}
              end)
              |> Map.new()

            {type, range_results}
          end)
          |> Map.new()
          |> IO.inspect()

        json(conn, all_results)
```

## Web Audio Player

Can play full songs in the web for a user, but doesn't have access to the full audio data

```js
import React, { useEffect, useState, useRef } from "react";
import PropTypes from "prop-types";
const debug = require("debug")("app:Test");

const SPOTIFY_TOKEN = "BQDpDPTaaaxAPycaj38UOEasxoQHmr91MIBfFge61aHjyJDLNDNqX-Dq1riXSrKhHSXv2ITgzbQuGBK4OkJvN0JWt6R_T7-pTUo3taxxn2nL33hNljzyl2czWGqBBmjcx9HFk9hTD11Cq0OoHnjD-qujfffFau2ljX7nO0_Iw";

function Test(props) {
  const playerR = useRef(null);

  useEffect(() => {
    window.onSpotifyWebPlaybackSDKReady = () => {
      const player = new Spotify.Player({
        name: "Spotify Cat Player",
        getOAuthToken: (cb) => {
          cb(SPOTIFY_TOKEN);
        },
      });

      // Error handling
      player.addListener("initialization_error", ({ message }) => {
        console.error(message);
      });
      player.addListener("authentication_error", ({ message }) => {
        console.error(message);
      });
      player.addListener("account_error", ({ message }) => {
        console.error(message);
      });
      player.addListener("playback_error", ({ message }) => {
        console.error(message);
      });

      // Playback status updates
      player.addListener("player_state_changed", (state) => {
        debug("player_state_changed", state);
      });

      // Ready
      player.addListener("ready", ({ device_id }) => {
        debug("Ready with Device ID", device_id);
        play({
          playerInstance: player,
          spotify_uri: "spotify:track:6Gu1BaGI5ijqEqK3g6gvMi",
        });
        navigator.mediaDevices
          .getDisplayMedia({ audio: true, video: true })
          .then((d) => debug("GET DISPLAY", d))
          .catch((err) => {
            debug("FAILED TO GET");
            console.error(err);
          });
      });

      // Not Ready
      player.addListener("not_ready", ({ device_id }) => {
        debug("Device ID has gone offline", device_id);
      });

      player.connect().then(() => {
        debug("CONNECTED PLAYER");
      });

      playerR.current = player;
    };
  }, []);

  return <div> Test </div>;
}

const play = ({
  spotify_uri,
  playerInstance: {
    _options: { getOAuthToken, id },
  },
}) => {
  getOAuthToken((access_token) => {
    debug("FETCHED access_token", access_token);
    fetch(`https://api.spotify.com/v1/me/player/play?device_id=${id}`, {
      method: "PUT",
      body: JSON.stringify({ uris: [spotify_uri] }),
      headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${access_token}`,
      },
    })
      .then((resp) => debug("GOT it", resp))
      .catch(console.error);
  });
};

Test.propTypes = {};
export default Test;

```

