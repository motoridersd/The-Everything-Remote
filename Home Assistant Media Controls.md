It's possible to deep link a title (movie or series) in Jellyfin through an ADB command

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

This uses a script for looking up the media ID in Jellyfin

Reference for adb command: https://github.com/jellyfin/jellyfin-androidtv/discussions/3452#discussioncomment-10927962

Sending special commands to the Shield/Android TV can be done via ADB, they are slow. Haven't found the BLE keyboard equivalent, but the Play/Pause button can be sent with an adb command:

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

Plex needs to be open for the Select Media to work from Home Assistant. Maybe launch the app and then you can select the item.

Mentioned in Reddit: https://www.reddit.com/r/PleX/comments/v9qeho/android_deep_linking_using_linksplextv/

100% Agree with you on that, I did find a less elegant way to acheive this, powering on the shield with android remote, then "launching" plex with this command"plex://play/?metadataKey=%2Flibrary%2Fmetadata%2F210002&metadataType=1&server=18faf9b995de929c36e2b10c3d73576f72fe3306" and then using the plex integration to trigger playing something on the plex app with this command "{ "library_name": "TV Shows", "show_name": "Rick and Morty", "season_number": 2, "episode_number": 7 }" 
