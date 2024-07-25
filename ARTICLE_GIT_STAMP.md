# Git Stamp - Flutter advanced versioning tool

## Introduction

In the standard approach to software development, we release subsequent versions by increasing versions.
It used to be version 1, 2, 3... Then someone came up with the idea of ​​making 2 parts of the version major.minor.
An example here is the famous Windows 3.11.
Currently, the most popular division is into three parts: major.minor.patch.
https://en.wikipedia.org/wiki/Software_versioning

This is all with a single-branch approach.
If we have software for multiple platforms and these platforms are divided into many more subplatforms, everything becomes more complicated.
An example here is the game for PC, PlayStation, XBOX and Android + iOS.
It should be possible to run a game from PS4 on PS5 for compatibility reasons, but usually the developers want this game to use new functions on the PS5 console, e.g. RayTracing or haptic functions in the new pad.
In the example of Minecraft, we most likely have some common code and some Android, iOS, XBOX...

If we introduce corrections to system notifications at the iOS level, we raise the version from 1.20.50 to 1.20.51.
The first common problem that occurs is the lack of `git push` or `git pull`. There is a solution to this in the form of entering the last commit `SHA` into the application while building.
A bigger problem is a complicated GitHub Actions script or similar tool. Then we are not sure whether everything was downloaded due to various cache mechanisms and whether it jumped to the branch we wanted.
In this case, a smart solution is to save the hash and branch to the final Android / PS5... build.

Using Minecraft as an example:
```
Version: v1.20.81
Build: 24130126
Branch: r/20_u8
SHA: a9081c5429038dcf3f26269f7351d89f
```

The `version number` and `build number` are the default.

The `branch` and `SHA` are additionally.

Of course, we can generate it manually using a `makefile`.

```
build:
	@echo 'export const VERSION = `$(GIT_TAG)`' > version.js
```

Or we can also use a `Git Stamp` tool.

## Usage

Just add the package to your flutter project and run the generator:
```dart
dart pub add git_stamp
dart run git_stamp
```

Example code:
```dart
import 'git_stamp/git_stamp.dart';

Text('Version: ${GitStamp.appVersion}'),
Text('Build: ${GitStamp.appBuild}'),
Text('Branch: ${GitStamp.buildBranch}'),
Text('SHA: ${GitStamp.latestCommit.hash}'),
```

In addition to simple information such as `build date`, the tool has a user interface that is compiled into the application with a list of commits and changes.
More on the project website:

https://pub.dev/packages/git_stamp

Source:
https://github.com/arononak/pagedout-institute/blob/main/ARTICLE_GIT_STAMP.md
