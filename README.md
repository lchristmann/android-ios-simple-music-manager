# Simple Music Manager - Mobile App (Android/iOS)

## Features Description

The App has a Bottom Navigation Bar

- bottom navbar with Piano, Guitar and Singing (the active thing is saved across sessions)
- there's a list view of collections (like playlists), you can create, edit (rename) and delete them
    - they hold 0 or many pieces (like a piano piece or a song), you can view, create edit and delete them)
      a song has a title, an artist/band name, can have a link, and some text (notes by the user)
- there's a 4th item in the bottom bar: compilations
  here you can add the songs from Guitar/Piano/Singing into compilations (like collections)
  a collection has a status (playable (green), wip (yellow), can't play yet (red))

## Environment Setup

Follow [the instructions](https://nativephp.com/docs/mobile/2/getting-started/environment-setup) on the NativePHP website -
just the **Requirements** and **Android Requirements** sections is enough.

For me having installed Android Studio, the `$JAVA_HOME` environment variable is already present and contained in the `PATH`, set to tmy OpenJDK 17 Java version.

For the other two variables I did:

```shell
export ANDROID_HOME=$HOME/Android/Sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/platform-tools
source ~/.bashrc
```

> Put those export commands in the ~/.bashrc if needed often.  

## Architecture

- NativePHP Mobile
- Laravel 12
- Laravel Livewire 4
- Tailwind CSS 4
- SQLite database

## Implementation Notes

- use the native [EDGE Component](https://nativephp.com/docs/mobile/2/edge-components/introduction) (platform-native UI element) [Bottom Navigation](https://nativephp.com/docs/mobile/2/edge-components/bottom-nav) 
