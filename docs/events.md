## Events
You can listen to video player events like:
```dart
  initialized,
  play,
  pause,
  seekTo,
  openFullscreen,
  hideFullscreen,
  setVolume,
  progress,
  finished,
  exception,
  controlsVisible,
  controlsHiddenStart,
  controlsHiddenEnd,
  setSpeed,
  changedSubtitles,
  changedTrack,
  changedPlayerVisibility,
  changedResolution,
  pipStart,
  pipStop,
  setupDataSource,
  bufferingStart,
  bufferingUpdate,
  bufferingEnd,
  changedPlaylistItem
```

After creating `BetterPlayerController` you can add event listener this way:
```dart
_betterPlayerController.addEventsListener((event){
    print("Better player event: ${event.betterPlayerEventType}");
});
```
Your event listener will be removed on dispose time automatically.

### Exception event parameters
For `BetterPlayerEventType.exception`, `event.parameters` contains the full exception as a string so you can show different popups (e.g. network vs DRM):
- **`exception`** – Full exception message (same as `message`).
- **`message`** – Full exception message string from the platform.

Example: show different popups based on the exception text (e.g. network, timeout, DRM):
```dart
_betterPlayerController.addEventsListener((event) {
  if (event.betterPlayerEventType == BetterPlayerEventType.exception) {
    final String? msg = event.parameters?['message'] ?? event.parameters?['exception'];
    if (msg != null) {
      if (msg.toLowerCase().contains('network') || msg.contains('Unable to connect') || msg.contains('SocketTimeout')) {
        // Show network error popup
      } else if (msg.toLowerCase().contains('drm')) {
        // Show DRM error popup
      } else {
        // Generic error popup
      }
    }
  }
});
```
