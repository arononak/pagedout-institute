# Git Stamp - Flutter advanced versioning tool

In the standard approach to software development, we release subsequent versions by increasing versions.
An example here is the famous Windows 3.11.
Currently, the most popular division is into three parts: major.minor.patch.
https://en.wikipedia.org/wiki/Software_versioning

This is all with a single-branch approach.
If we have software for multiple platforms and these platforms are divided into many more subplatforms, everything becomes more complicated.
An example here is the game for PC, PlayStation, XBOX and Android + iOS.
It should be possible to run a game from PS4 on PS5 for compatibility reasons, but usually the developers want this game to use new functions on the PS5 console, e.g. RayTracing or haptic functions in the new pad.
In the example of Minecraft, we most likely have some common code and some Android, iOS, XBOX...

If we introduce corrections to system notifications at the iOS level, we raise the version from 1.20.50 to 1.20.51, but what if we change something in the common part? and these versions are most likely not built manually and there is one repository with the core part, downloaded to all other Android, PS5 ... most likely as ```git submodule``` and we are not sure whether these fixes have been downloaded due to cache mechanisms ?
In this case, a smart solution is to save the hash and branch to the final Android / PS5... build.

Using Minecraft as an example:
```
Version: v1.20.81
Build: 24130126
Branch: r/20_u8
SHA: a9081c5429038dcf3f26269f7351d89f
```

By default, they added: `version number` and `build number`. Additionally, they added `branch` and `SHA`. Useful for manual testing.

Such a file with HASH can be created during building with a makefile:
```
build:
	@echo 'export const VERSION = `$(GIT_TAG)`' > version.js
```

Source:
https://github.com/arononak/github-actions-gnome-extension/blob/main/makefile

There are also more advanced solutions, and an example is my Flutter package `git_stamp`.
Which will generate more complicated code.
From simple information such as `build date`, `branch` and `hash` to the entire screen with history and changes.
https://pub.dev/packages/git_stamp

The mechanism of action is very simple. Similar to the Dagger code generator for creating a dependency graph. Useful for manual testing. All you need to do is replace one object and the environment changes from PROD to TESTING.
https://dagger.dev

Just add the package to your flutter project and run the generator:
```dart
dart pub add git_stamp
dart run git_stamp
```

Unfortunately, for now it is only available on the Flutter platform :/
