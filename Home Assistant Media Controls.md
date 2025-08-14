It's possible to deep link a title (movie or series) in Jellyfin through an ADB command

Reference for adb command: https://github.com/jellyfin/jellyfin-androidtv/discussions/3452#discussioncomment-10927962

```
data:
  command: >-
    adb shell am start -c android.intent.category.LEANBACK_LAUNCHER -a
    android.intent.action.VIEW -d "{{jellyfin_media_id.media_id}}" -e source 30
    org.jellyfin.androidtv/.ui.startup.StartupActivity
target:
  entity_id: media_player.nvidia_shield
action: androidtv.adb_command
```

This uses a [script](https://github.com/motoridersd/The-Everything-Remote/blob/main/Find%20Jellyfin%20Media%20ID.script) for looking up the media ID in Jellyfin. The script is called in an automation

A restful entry needs to be added to the configuration.yaml

```
rest_command:
  jellyfin_search:
    url: "http://{jellyfin_IP}:8096/Items?api_key={user_API_KEY}&searchTerm={{ search_string }}&Recursive=true&IncludeMedia=true&IncludeItemTypes={{ type }}"
    method: GET
```

I made this work through information on the Home Assistant Community https://community.home-assistant.io/t/how-to-play-jellyfin-movies-on-nvidia-shield-via-home-assistant-voice/868219/4?u=motoridersd

The script is triggered via an action:

```
  - action: script.find_jellyfin_media_id
    metadata: {}
    data:
      f_media_type: Movie
      f_search_string: "{{trigger.slots.movie_title}}"
    response_variable: jellyfin_media_id
```

One has to specify the kind of media, so "Movie" or "Shows"

Sending special commands to the Shield/Android TV can be done via ADB, they are slow. Haven't found the BLE keyboard equivalent of Play/Pause, but it can be sent with an adb command:

```
action: androidtv.adb_command
metadata: {}
data:
  command: input keyevent 85
target:
  entity_id: media_player.nvidia_shield
```

This command can be sent after the deeplink, since that will only pull up the media and wait for user input to start playback.

85 is play/pause
126 is play

Making this work in Plex is a lot more complicated with the Shield (and other Android TV devices probably) because as soon as the Shield stops playing something, it becomes unavailable in Home Assistant. When it is playing media, you can browse and search media.

Plex needs to be open for the Select Media to work from Home Assistant. Maybe launch the app and then you can select the item. The Stock Pot has some methodology used with Plex: https://www.thestockpot.net/videos/cartrdgeplayer

This method was mentioned on Reddit but haven't tested it: https://www.reddit.com/r/PleX/comments/v9qeho/android_deep_linking_using_linksplextv/

100% Agree with you on that, I did find a less elegant way to acheive this, powering on the shield with android remote, then "launching" plex with this command"plex://play/?metadataKey=%2Flibrary%2Fmetadata%2F210002&metadataType=1&server=18faf9b995de929c36e2b10c3d73576f72fe3306" and then using the plex integration to trigger playing something on the plex app with this command "{ "library_name": "TV Shows", "show_name": "Rick and Morty", "season_number": 2, "episode_number": 7 }" 
