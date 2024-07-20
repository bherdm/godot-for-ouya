# godot-for-ouya

godot-for-ouya aims to provide the best experience for making new OUYA games.

## Engine Setup

### Video Overview for Windows 11

[![Link to Godot for Ouya - Windows 11 Overview](https://img.youtube.com/vi/Ea1bsJfZyj4/hqdefault.jpg)](https://www.youtube.com/watch?v=Ea1bsJfZyj4 "Windows 11 Overview")


### Install OpenJDK 17

Download and install [OpenJDK 17](https://adoptium.net/?variant=openjdk17).

Compiling for OUYA requires Java 8, but the latest Android command line tools requires a later version of Java.

### Download the Android SDK

Download the latest command line tools for the Android SDK, found near the bottom of [this page](https://developer.android.com/studio).

Extract the contents to wherever/Android/sdk/cmdline-tools/latest

In terminal, navigate to wherever/Android/sdk/cmdline-tools/latest/bin and install the necessary packages.

 ```./sdkmanager "platforms;android-23" "platform-tools" "build-tools;26.0.1" "ndk;17.2.4988734" "sources;android-23"```

Accept the licenses.

```./sdkmanager --licenses```

### Install OpenJDK 8

Download and install [OpenJDK 8](https://adoptium.net/?variant=openjdk8).

### Create a debug.keystore

Android needs a debug keystore file to install to devices and distribute non-release APKs. If you have used the SDK before and have built projects, ant or eclipse probably generated one for you (In Linux and OSX, you can find it in the ~/.android folder).

If you can’t find it or need to generate one, the keytool command from the JDK can be used for this purpose:

```keytool -keyalg RSA -genkeypair -alias androiddebugkey -keypass android -keystore debug.keystore -storepass android -dname "CN=Android Debug,O=Android,C=US" -validity 9999```

### Download the Engine and Android Templates

Download the engine and Android template APKs from the [releases page](https://github.com/bherdm/godot-for-ouya/releases).

Extract the zip files.

### Download the Stable Export Templates

Download the [2.1.6-stable_export_templates.tpz](https://github.com/godotengine/godot/releases/tag/2.1.6-stable).

### Godot Export Configuration

Open Godot for OUYA. In Editor Settings, set these 3 file paths:

* Android SDK's _adb_.
* OpenJDK 8's _jarsigner_.
* Your debug _keystore_.

Import the stable export templates.

#### Project Export Settings

Set the Android export custom debug/release packages to the extracted APKs from the [releases page](https://github.com/bherdm/godot-for-ouya/releases).

Set a unique package name with syntax: com.companyname.productname

Set the OUYA icon. The OUYA icon should be a 732x412 PNG imported into the project assets.

## Community

For more information on the OUYA and the OUYA community, visit https://ouya.world/ and the OUYA Saviors Discord server https://discord.gg/Sdhhuw2.

## What's next?

It's my intention to use this repository to build the best engine available for OUYA. I plan to build my own fork from the official Godot source code and gradually backport quality of life features from Godot 3 to **godot-for-ouya**.

The first major milestone will be supporting engine compilation on modern Mac OS and the editor running on Apple Silicon Macs.

[![GODOT](/logo.png)](https://godotengine.org)

## Godot Engine

Homepage: https://godotengine.org

#### 2D and 3D cross-platform game engine

Godot Engine is a feature-packed, cross-platform game engine to create 2D and
3D games from a unified interface. It provides a comprehensive set of common
tools, so that users can focus on making games without having to reinvent the
wheel. Games can be exported in one click to a number of platforms, including
the major desktop platforms (Linux, Mac OSX, Windows) as well as mobile
(Android, iOS) and web-based (HTML5) platforms.

#### Free, open source and community-driven

Godot is completely free and open source under the very permissive MIT license.
No strings attached, no royalties, nothing. The users' games are theirs, down
to the last line of engine code. Godot's development is fully independent and
community-driven, empowering users to help shape their engine to match their
expectations. It is supported by the Software Freedom Conservancy
not-for-profit.

Before being open sourced in February 2014, Godot had been developed by Juan
Linietsky and Ariel Manzur (both still maintaining the project) for several
years as an in-house engine, used to publish several work-for-hire titles.

### Getting the engine

#### Binary downloads

Official binaries for the Godot editor and the export templates can be found
[on the homepage](https://godotengine.org/download).

#### Compiling from source

[See the official docs](http://docs.godotengine.org/en/latest/development/compiling/)
for compilation instructions for every supported platform.

### Community

Godot is not only an engine but an ever-growing community of users and engine
developers. The main community channels are listed [on the homepage](https://godotengine.org/community).

To get in touch with the developers, the best way is to join the
[#godotengine IRC channel](https://webchat.freenode.net/?channels=godotengine)
on Freenode.

### Documentation and demos

The official documentation is hosted on [ReadTheDocs](http://docs.godotengine.org).
It is maintained by the Godot community in its own [GitHub repository](https://github.com/godotengine/godot-docs).

The [class reference](http://docs.godotengine.org/en/latest/classes/)
is also accessible from within the engine.

The official demos are maintained in their own [GitHub repository](https://github.com/godotengine/godot-demo-projects)
as well.

There are also a number of other learning resources provided by the community,
such as text and video tutorials, demos, etc. Consult the [community channels](https://godotengine.org/community)
for more info.

[![Build Status](https://travis-ci.org/godotengine/godot.svg?branch=master)](https://travis-ci.org/godotengine/godot)
[![Code Triagers Badge](https://www.codetriage.com/godotengine/godot/badges/users.svg)](https://www.codetriage.com/godotengine/godot)
