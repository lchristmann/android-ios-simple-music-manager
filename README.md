# Simple Music Manager - Mobile App (Android/iOS)

## ⚠️ Mission Aborted

For both Windows and Linux it's at the point now where I quickly solved a ServiceProviders not found error in the absurd way to move
a bunch of dev dependency's (Collision, Pest, Sail,...) to prod dependencies (because NativePHP needed to have it running with the application code apparently)

And even with that solved, the app won't open, but exits instantly.

With both tries being unsuccessful and half a day spent tinkering around with NativePHP, I'll stay away from the tech for now and watch what progress will get made, to maybe use it later when it's further down the road better battle-tested and potentially well-documented for Linux Ubuntu.

> The best thing I'd love to see would really be an official Docker-based development setup replacing all of those tedious manual
> installations, configurations and environment variable setting. That would work for all operating systems. But has its own challenges of course... (e.g. regarding phone emulation).

## Features Description

The App has a Bottom Navigation Bar where variable instruments (e.g. guitar, piano,vocals) are listed (user-defined).
The currently active menu item is saved across sessions (so when last time you used the app, you had the "guitar" view open,
next time you open the app it'll be open still.

Now on the screen for each of these menu items, there's a list of collections (you can add, rename and delete them).

These collections hold "pieces" (like a piano piece or a song). You can view, create, edit and delete them.
A piece has a name, an artist, can have a link and some text (notes by the user).
When there's a link filled, it shall be set on the collection list item, so you'll get quickly led to the song's guitar tab webpage for example.

There's another special Bottom Navigation Bar item: "Compilations". Here you can add the songs from your instrument collections
into Playlists, that can have a status (playable, working on it, can't play yet)).

## Environment Setup

Follow [the instructions](https://nativephp.com/docs/mobile/2/getting-started/environment-setup) on the NativePHP website -
just the **Requirements** and **Android Requirements** sections is enough.

### Linux Ubuntu

For me having installed Android Studio, the `$JAVA_HOME` environment variable is already present and contained in the `PATH`, set to tmy OpenJDK 17 Java version.

For the other two variables I did:

```shell
export ANDROID_HOME=$HOME/Android/Sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/platform-tools
source ~/.bashrc
```

> Put those export commands in the ~/.bashrc if needed often.  

### Windows

```shell
$env:ANDROID_HOME = "C:\Users\leand\AppData\Local\Android\Sdk"
$env:PATH += ";$env:ANDROID_HOME\platform-tools"
$env:PATH += ";$env:ANDROID_HOME\emulator"
```

> Like with the above Linux Ubuntu solution, this is temporary too.

For the `php artisan native:run` command to not exit during the stage "Optimizing autoloader", execute:

```shell
setx COMPOSER_PROCESS_TIMEOUT 300
```

### Both Windows and Linux

```shell
cp .env.example .env # for Linux just do this Ctr++C  Ctr+V
composer install
npm install && npm run build # Linux Ubuntu
npm install; npm run build
php artisan native:install
# Before running this edit the vendor/nativephp/mobile/src/Traits/PreparesBuild.php Trait, line 256 say ->timeout(300) instead of ->timeout(60) for the composer dump-autoload command
php artisan native:run
```

## Architecture

- NativePHP Mobile
- Laravel 12
- Laravel Livewire 4
- Tailwind CSS 4
- SQLite database

## Implementation Notes

- use the native [EDGE Component](https://nativephp.com/docs/mobile/2/edge-components/introduction) (platform-native UI element) [Bottom Navigation](https://nativephp.com/docs/mobile/2/edge-components/bottom-nav) 
