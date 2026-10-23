# File for HEY releases

The signed, notarised builds of [File for HEY](https://toolsforhey.com/file), a
Mac app by Soules Studio Ltd that keeps a folder of your HEY attachments. The
source is not public. Issues are open here for bug reports and questions about
the app, and support@soulesstudio.com reaches the same person.

File for HEY is an unofficial Mac app built on top of the official HEY CLI. Not
affiliated with 37signals. HEY is a trademark of 37signals.

What the app keeps on your Mac, what it sends and how to remove all of it is on
[toolsforhey.com/file/privacy](https://toolsforhey.com/file/privacy).

## What is here

One GitHub release per app release, tagged by version, for example `file-1.0.0`.

Each release carries two copies of the same disk image. `FileForHEY-<version>.dmg`
is the one people download from the website, and `FileForHEY-<version>-update.dmg`
is the one the app downloads when it updates itself, so installs and updates are
counted apart. Downloads for people belong on
[toolsforhey.com/file](https://toolsforhey.com/file), which is where the app is
actually described. This repository is where the file itself is served from.

The app bundles the official `hey` command line tool from
[github.com/basecamp/hey-cli](https://github.com/basecamp/hey-cli), MIT licensed
by 37signals. The licence text ships inside the app.

## Why the binaries are here and not on the website

The app updates itself through Sparkle, which downloads the whole disk image on
every update for every existing user. Serving that from the website would attach
a metered, uncappable bill to the app being popular. GitHub does not meter
release downloads.

## Never delete or rename a release asset

Every published update feed contains the download URL of the disk image it
describes. An installed copy on an old version asks for that exact URL when it
updates. Delete or rename the asset and that copy can never update again,
silently, with no way back except asking the user to download the app by hand.

Assets here are append only. A bad release is superseded by a new one, never
removed.

## Verifying a download

Every disk image is signed with a Developer ID certificate and notarised by
Apple. To check a download yourself, either compare its SHA-256 with the digest
GitHub shows beside the asset, or ask macOS who signed it:

```
spctl -a -t open --context context:primary-signature -vv FileForHEY-1.0.0.dmg
```

It should answer `accepted` and `source=Notarized Developer ID`. Inside the
image, this should name the Developer ID certificate of Soules Studio, team
identifier 93XLFSVNZ7:

```
codesign -dv --verbose=2 "/Volumes/File for HEY/File for HEY.app"
```
