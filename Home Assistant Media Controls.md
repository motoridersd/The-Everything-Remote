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
