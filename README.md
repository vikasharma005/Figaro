<p align="center">
  <img alt="Figaro" src="media/figaro.png" width="125" height="125" />
</p>
<h1 align="center">Figaro</h1>
<p align="center">
  <img alt="GitHub" src="https://img.shields.io/github/license/MattMoony/figaro?style=for-the-badge">
  <img alt="GitHub top language" src="https://img.shields.io/github/languages/top/MattMoony/figaro?style=for-the-badge">
  <img alt="GitHub Repo stars" src="https://img.shields.io/github/stars/MattMoony/figaro?style=for-the-badge&color=cecece">
</p>

---

## About

Real-time open-source voice modification program & sound board. Can be useful for many things, especially when used in combination with virtual sound i/o devices.

![figaro collage](media/figaro-collage.png)

## Table of Contents

- [About](#about)
- [Table of Contents](#table-of-contents)
- [Setup](#setup)
  - [Development](#development)
    - [Linux](#linux)
    - [Mac](#mac)
    - [Windows](#windows)
    - [Manual Setup](#manual-setup)
  - [Advanced setup](#advanced-setup)
- [Usage](#usage)
  - [CLI](#cli)
  - [GUI](#gui)
  - [Figaro-Script](#figaro-script)
    - [General Syntax](#general-syntax)
    - [Defining a Hotkey](#defining-a-hotkey)
    - [Comments](#comments)
    - [Builtins](#builtins)
      - [Pause](#pause)
- [Roadmap](#roadmap)
- [References](#references)

## Setup

If you're just looking to use *Figaro* and not work on it, then there's no reason to set up the development environment like described below, simply download the appropriate release for your platform from the [releases](https://github.com/vikasharma005/Figaro/releases) page and you're good to go!

<div align="center">
  <a href="https://github.com/vikasharma005/Figaro/releases/download/alpha/Figaro.Setup.0.3.0-alpha.exe"><img src="media/download-windows.png" height="75px" /></a>
  <a href="https://github.com/vikasharma005/Figaro/releases/download/v0.3-alpha/figaro-gui-0.3.0-alpha.tar.gz"><img src="media/download-linux.png" height="75px" /></a>
</div>

### Development

If you're on `Linux`, `Windows` or `Mac`, then setting up should be easy! Simply run the appropriate setup script and it will guide you through the whole process.

#### Linux

Make `./setup.sh` executable ... (or run it with an appropriate interpreter) ...

```bash
chmod 755 ./setup.sh
```

... execute it: `./setup.sh` ... and have fun with `python figaro.py`!

#### Mac

The same as the [Linux Setup](#linux), just use `./setup-mac.sh` instead of `./setup.sh`.

#### Windows

First, in order to allow the setup _powershell_ script to run, you need to execute the following command in an administrator powershell:

```ps
Set-ExecutionPolicy RemoteSigned
```

... afterwards, executing `.\setup.ps1` will guide you through the whole setup process! You can now execute `python figaro.py`.

#### Manual Setup

First of all, for `Figaro` to be able to work with audio files other than `wav`, you need to download and install `ffmpeg`.

- **Linux**: `pip install -r requirements-unix.txt`
- **Mac**: `pip install -r requirements-unix.txt`
- **Windows**: `pip install -r requirements-windows.txt`

... if you're on **Windows** and you get an error when installing `PyAudio` try downloading a PIP wheel suitable for your Python version.

If everything works out, you're good to go!

### Advanced setup

The following steps will explain how to use this program with the commonly used voice-chat application `Discord` on Windows:

1. Download and install a virtual audio input device.
2. When selecting an output device at the startup of `Figaro`, choose the virtual input device you just installed (e.g.: `CABLE Input`).
3. In Discord, go to `User Settings > Voice & Video > Input Device` and select the virtual input device from the dropdown (e.g.: `CABLE Output`).
4. There you go, your friends should only be able to hear your filtered voice now.

## Usage

### CLI

CLI-Usage is explained [here](https://github.com/vikasharma005/Figaro/blob/main/docs/cli.md).

### GUI

GUI-Usage is explained [here](https://github.com/vikasharma005/Figaro/blob/main/docs/gui.md).

### Figaro-Script

You can now also use figaro script (.fig) for defining hotkeys and their behaviour. Whether you want a sound effect to be played, or an attribute to be shown, it can all be bound to a certain keypress.

#### General Syntax

Figaro-Script was heavily inspired by [AutoHotkey](https://www.autohotkey.com/), so, if you are capable of defining hotkeys and their functionality with ahk-script, think of this as a very, very simplified version of that.

But, if you aren't aware of AHK, let me introduce you to the basic syntax very quickly:

Your script, the.fig file, consists of multiple hotkey-definition blocks that tell Figaro which key combinations should result in what behavior. Apart from that, you can also have comments to make your script more readable and easier to understand for future readers.

#### Defining a Hotkey

In order to define which keys make up your hotkey, you just need to write all of them in one line and end it with `::`. After this first line, you write all your commands and end the definition block with `return`. This could look something like the following:

```text
...

q::
start sound tmp/asdf.mp3 2
return

...
```

This hotkey would be triggered every time the `q` is pressed.

Certain control keys need alternative symbols (this is equivalent to ahk-script):

* `alt` is represented by `!`
* `ctrl` is represented by `^`
* `shift` is represented by `+`

Keep in mind that the definition of hotkeys is usually case insensitive, which means in order to, for example, only trigger the hotkey on an uppercase `Q`, you would need to use `+q::` as your definition.

#### Comments

This is fairly easy to explain. If you have ever used a popular programming language such as C, C++, Java, etc. you already know how to use comments. The only thing to bear in mind is that so far, I have only implemented `single-line` comments.

For people who have never used such a programming language before, this is the correct syntax for comments in Figaro-Script:

```text
...

// triggered by pressing `lower-case q`
// will play the mp3 file "tmp/asdf.mp3" at 200% of the original volume ...
q::
start sound tmp/asdf.mp3 2
return

...
```

#### Builtins

Despite the CLI commands, certain builtin functions are also available to you (at the moment there aren't many, but I will at more should the need to do so arise):

##### Pause

You can use this command in order play a sound effect, or do anything else for that matter, after waiting for a given amount of `milliseconds`. E.g.:

```text
...
start sound tmp/1.mp3
pause 3000
start sound tmp/2.mp3
...
```

... this would play the sound effect `tmp/1.mp3`, wait for `3 seconds` and then play the next sound effect `tmp/2.mp3`.

_More docs coming soon! Disclaimer: Some of the commands described above might still be removed or altered..._

## Roadmap

Just a small preview of what is about to come. It's very likely that this roadmap will continue to grow in the future, as I get more ideas or if somebody wants to contribute.

* [x] [CLI](#cli)
  * [x] I/O device selection
  * [x] Live status (live audio graph in console)
  * [x] Filter control
  * [x] Sound effects (soundboard-like abilities)
* [ ] [GUI](#gui)
  * [x] I/O device selection
  * [x] Live sound wave graph
  * [x] Filter control
  * [ ] Soundboard
    * [x] Functionality
    * [ ] Advanced features
* [x] Filters
  * [x] Volume
  * [x] Pitch-Shift
  * [x] "Trippy"-Filter
  * [x] Echo
  * [x] Noise
  * [x] Crackle
  * [x] Randomized
* [ ] [Figaro-Script](#figaro-script)
  * [x] Using CLI commands
  * [x] Hotkeys
  * [ ] Advanced builtins
* [ ] Security
  * [x] Remote Authentication
  * [x] Encrypted sockets
  * [ ] Fine-grained settings

## Author

<div id="header" align="center">
  <img src="https://media.giphy.com/media/M9gbBd9nbDrOTu1Mqx/giphy.gif" width="100"/>
</div>

<h3 align="center">Hi there 👋, I'm Vikas</h3>
<h4 align="center">Just learning New Skills😀</h4>

<div id="socials" align="center">
  <a href="https://www.linkedin.com/in/vikas-sharma005">
    <img src="https://user-images.githubusercontent.com/76098066/186728913-a66ef85f-4644-4e3a-b847-98309c8cff42.svg">
  </a>
  <a href="https://www.instagram.com/_thisisvikas">
    <img src="https://user-images.githubusercontent.com/76098066/186728908-f1a9919a-f4b2-4262-9515-683e77f8aabf.svg">
  </a>
  <a href="https://twitter.com/hitechvikas05">
    <img src="https://user-images.githubusercontent.com/76098066/186728901-a4d90f01-2cdf-45c1-a1b3-73467c3d2698.svg">
  </a>
</div>

You can find more about me and my projects on my [GitHub profile](https://github.com/vikasharma005).
