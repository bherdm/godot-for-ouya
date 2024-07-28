# Godot-for-OUYA

## Engine Setup

<details> 
  <summary>All Downloads</summary>

OpenJDK 8<br>
[Windows](https://adoptium.net/temurin/releases/?os=windows&version=8 "https://adoptium.net/temurin/releases/?os=windows&version=8") - [Mac](https://adoptium.net/temurin/releases/?os=mac&version=8 "https://adoptium.net/temurin/releases/?os=mac&version=8")

Android SDK Command Line Tools v8.0<br>[Windows](https://dl.google.com/android/repository/commandlinetools-win-9123335_latest.zip "https://dl.google.com/android/repository/commandlinetools-win-9123335_latest.zi") - [Mac](https://dl.google.com/android/repository/commandlinetools-mac-9123335_latest.zip "https://dl.google.com/android/repository/commandlinetools-mac-9123335_latest.zip")

Godot-for-OUYA Engine + Android Template APKs<br>
https://github.com/bherdm/godot-for-ouya/releases/tag/ouya-2.1.7-rc-ville2304

Official Godot Engine 2.1.6-stable Export Templates<br>
https://github.com/godotengine/godot/releases/tag/2.1.6-stable
</details>


### JDK 8

Allow the installer to add Java to the environment path. Oracle's JDK 8 also works.

### Android SDK

Recent versions of the Android SDK command line tools require a recent version of Java. To avoid needing two JDKs and two sets of command line tools, use the command line tools version 8.0.

Extract the command line tools with this folder structure:

```
/wherever/Android/sdk/cmdline-tools/latest/bin
/wherever/Android/sdk/cmdline-tools/latest/lib
/wherever/Android/sdk/cmdline-tools/latest/NOTICE.txt
/wherever/Android/sdk/cmdline-tools/latest/source.properties
```

Use Powershell to install the necessary Android SDK components.

```
cd /wherever/Android/sdk/cmdline-tools/bin

./sdkmanager "platforms;android-23" "platform-tools" "build-tools;26.0.1" "ndk;17.2.4988734" "sources;android-23"
```

Accept the licenses.

```
./sdkmanager --licenses
```

### Create a debug.keystore

Android needs a debug keystore file to install to devices and distribute non-release APKs. If you have used the SDK before and have built projects, ant or eclipse probably generated one for you (In Linux and OSX, you can find it in the ~/.android folder).

If you can’t find it or need to generate one, the keytool command from the JDK can be used for this purpose.

On Windows, use Powershell, opened as administrator.

On Mac, precede this command with ```sudo```.

```keytool -keyalg RSA -genkeypair -alias androiddebugkey -keypass android -keystore debug.keystore -storepass android -dname "CN=Android Debug,O=Android,C=US" -validity 9999```

### Engine Configuration for OUYA Export

Open Godot-for-OUYA. In Editor Settings, set these 3 file paths:

* Android SDK's _adb_.
    * /wherever/Android/sdk/platform-tools
* OpenJDK 8's _jarsigner_.
    * Windows: ```C:\Program Files\Eclipse Adoptium\jdk-8.0.412.8-hotspot\bin```
    * Mac OS: ```/Library/Java/JavaVirtualMachines/temurin-8.jdk/Contents/Home/bin```
* Your debug _keystore_.

Import the stable export templates.

#### Project Export Settings

Set the Android export custom debug/release packages to the extracted APKs from the [releases page](https://github.com/bherdm/godot-for-ouya/releases).

Set a unique package name with syntax: com.companyname.productname

Set the OUYA icon. The OUYA icon should be a 732x412 PNG imported into the project assets.

## Compiling the Engine

Follow this guide to compile the engine and export templates from source.

<details> 
  <summary>All Downloads</summary>

OpenJDK 8<br>
[Windows](https://adoptium.net/temurin/releases/?os=windows&version=8 "https://adoptium.net/temurin/releases/?os=windows&version=8") - [Mac](https://adoptium.net/temurin/releases/?os=mac&version=8 "https://adoptium.net/temurin/releases/?os=mac&version=8")

Android SDK Command Line Tools v8.0<br>[Windows](https://dl.google.com/android/repository/commandlinetools-win-9123335_latest.zip "https://dl.google.com/android/repository/commandlinetools-win-9123335_latest.zi") - [Mac](https://dl.google.com/android/repository/commandlinetools-mac-9123335_latest.zip "https://dl.google.com/android/repository/commandlinetools-mac-9123335_latest.zip")

Python 2.7.18 32-bit<br>
https://www.python.org/downloads/release/python-2718/

SCons 2.5.1<br>
https://sourceforge.net/projects/scons/files/scons/2.5.1/scons-2.5.1.zip/download

Godot-for-OUYA Source<br>
https://github.com/bherdm/godot-for-ouya.git

**Windows-Specific:**<br>
Visual Studio Community 2022<br>
https://visualstudio.microsoft.com/vs/community/

Pywin32 Python Extension<br>
(pywin32-221.win32-py2.7.exe)<br>
https://sourceforge.net/projects/pywin32/files/pywin32/Build%20221/

**Mac OS-Specific:**<br>
Xcode<br>
https://developer.apple.com/download/

</details>

### JDK 8

Allow the installer to add Java to the environment path. Oracle's JDK 8 also works.

### Android SDK

Recent versions of the Android SDK command line tools require a recent version of Java. To avoid needing two JDKs and two sets of command line tools, use the command line tools version 8.0.

Extract the command line tools with this folder structure:

```
/wherever/Android/sdk/cmdline-tools/latest/bin
/wherever/Android/sdk/cmdline-tools/latest/lib
/wherever/Android/sdk/cmdline-tools/latest/NOTICE.txt
/wherever/Android/sdk/cmdline-tools/latest/source.properties
```

Use Powershell to install the necessary Android SDK components.

```
cd /wherever/Android/sdk/cmdline-tools/bin

./sdkmanager "platforms;android-23" "platform-tools" "build-tools;26.0.1" "ndk;17.2.4988734" "sources;android-23"
```

Accept the licenses.

```
./sdkmanager --licenses
```

### Python 2.7.18 32-bit

Allow the installer to add Python to the environment path.

### SCons 2.5.1

Extract the zip. Open Powershell with admin access.

```
cd /Downloads/scons-2.5.1

python setup.py install
```

### Windows-Specific Requirements

#### Visual Studio Community 2022

From the Visual Studio Installer, select the "Desktop development with C++" workload.

In the right panel, also check the optional component "MSVC v140 - VS 2015 C++ build tools"



#### Pywin32 Python Extension

(pywin32-221.win32-py2.7.exe)

This component is optional, but allows for parallel builds (which increase the build speed by a great factor).

#### Environment Variables

From the Windows Start Menu, search "env" and open the result titled "Edit the system environment variables."

Click the Environment Variables button.

Add these variables to the user variables:

- ANDROID_JAVA_HOME=/path/to/java 8/Home
- ANDROID_HOME=/path/to/sdk/root
- ANDROID_NDK_ROOT=/path/to/NDK/root
- ANDROID_NDK_HOME=/path/to/NDK/root
- BUILD_REVISION=OUYA

<details> 
  <summary>These were likely already set by the program's installer.</summary>

- JAVA_HOME=/path/to/java 8/

- Path += /path/to/python27
</details>

### Mac OS-Specific Requirements

#### Xcode Command Line Tools

Install the Xcode Command Line Tools for your version of Mac OS.
<details>
    <summary>Tip: Do this without logging in.</summary>
    Install homebrew and the Xcode Command Line Tools by using this command in Terminal:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Bonus: Once you have homebrew, build and install the latest version of git. This may take awhile.

```
brew install git
```

</details>

#### Environment Variables

Create the variables file:

```
touch ~/.bash_profile
```

Open it in a text editor:

```
open -a TextEdit.app ~/.bash_profile
```

Be sure these variables and their paths are in the file. Replace /wherever/ with the path leading to your programs.

```
export ANDROID_JAVA_HOME=/Library/Java/JavaVirtualMachines/temurin-8.jdk/Contents/Home
export ANDROID_HOME=/wherever/.android/sdk
export ANDROID_NDK_ROOT=/wherever/.android/sdk/ndk/17.2.4988734
export ANDROID_NDK_HOME=/wherever/.android/sdk/ndk/17.2.4988734
export BUILD_REVISION=OUYA
```

Update environment variables in terminal:

```
source ~/.bash_profile
```

## Compiling

<details> 
  <summary>Notes about Windows and Visual Studio</summary>

SCons will not be able to compile from the standard
Windows "Command Prompt" or "Terminal" because SCons and Visual C++ compiler
will not be able to locate environment variables and executables they
need for compilation.

Therefore, you need to start a Visual Studio command prompt. It sets up
environment variables needed by SCons to locate the compiler.
It should be called similar to one of the names below:

- "x64 Native Tools Command Prompt for VS 2022"
- "x64_86 Cross Tools Command Prompt for VS 2022"
- "x86 Native Tools Command Prompt for VS 2022"
- "x86_64 Cross Tools Command Prompt for VS 2022"

If these did not appear in the Start Menu after installing, refer to the official [Godot 2.1 - Compiling for Windows](https://docs.godotengine.org/en/2.1/development/compiling/compiling_for_windows.html) page for additional troubleshooting.

### About the Developer/Tools Command Prompts and the Visual C++ compiler

There are a few things you need to know about these consoles and the
Visual C++ compiler.

Your Visual Studio installation will ship with several Visual C++
compilers, them being more or less identical, however each cl.exe
(Visual C++ compiler) will compile Godot for a different architecture
(32 or 64-bit, ARM compiler is not supported).

The **Developer Command Prompt** will build a 32-bit version of Godot by
using the 32-bit Visual C++ compiler.

**Native Tools** Prompts (mentioned above) are used when you want the
32-bit cl.exe to compile a 32-bit executable (x86 Native Tools
Command Prompt). For the 64-bit cl.exe, it will compile a 64-bit
executable (x64 Native Tools Command Prompt).

The **Cross Tools** are used when your Windows is using one architecture
(32-bit, for example) and you need to compile to a different
architecture (64-bit). As you might be familiar, 32-bit Windows can not
run 64-bit executables, but you still might need to compile for them.
</details>

### Running SCons

Using terminal in the root directory of the engine source code:

<details> 
  <summary>Tip: Parallel Builds</summary>
On Macs, and on Windows if you installed "Pywin32 Python Extension," you can append the -j
command to instruct SCons to run parallel builds like this:

```
scons platform=windows -j9
```

In general, it is OK to have at least as many threads compiling Godot as
you have cores in your CPU, if not one or two more, I use -j9
(nine threads) for my 8 core CPU, your mileage may vary.
</details>

#### Windows Editor

```
scons platform=windows
```

#### Mac OS Editor

```
scons platform=osx target=release_debug bits=64

cp -r misc/dist/osx_tools.app ./godot-for-ouya.app
mkdir -p godot-for-ouya.app/Contents/MacOS
cp bin/godot.osx.opt.tools.64 godot-for-ouya.app/Contents/MacOS/Godot
chmod +x godot-for-ouya.app/Contents/MacOS/Godot

scons platform=osx target=release_debug bits=32

cp -r misc/dist/osx_tools.app ./godot-for-ouya.app
mkdir -p godot-for-ouya.app/Contents/MacOS
cp bin/godot.osx.opt.tools.32 godot-for-ouya.app/Contents/MacOS/Godot
chmod +x godot-for-ouya.app/Contents/MacOS/Godot
```

#### Android Templates

```
scons platform=android target=debug android_arch=armv7
scons platform=android target=release android_arch=armv7
```

### Running Gradle

After running SCons, compile the Android Template APKs.

```
cd platform/android/java

gradlew build
```

## Community

For more information on the OUYA and the OUYA community, visit https://ouya.world/ and the OUYA Saviors Discord server https://discord.gg/Sdhhuw2.

## What's next?

It's my intention to build a future-proof game dev environment to continue the OUYA revolution forever. The most critical goals of this project include modernizing the build system so that modern Unix systems can be used to contribute to the engine, as well as adding support for the editor to run and export on Apple Silicon Macs.

## Godot Engine

[![GODOT](/logo.png)](https://godotengine.org)

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