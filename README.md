# Atomiix

Atomiix is a re-implementation of the Ixi lang live-coding environment.

The documentation already assumes some knowledge of Ixi lang, and needs to be greatly improved.

There are also bugs, though things are about at the stage where it's usable and hopefully useful.


## Installation

Atomiix has two parts, the audio engine written in SuperCollider and the Atom editor plug-in.

Installing SuperCollider should just involve going to the [Download](https://supercollider.github.io/download) page on the website, downloading the most recent version for your platform, and then running the installer.
The [SC3 Plugins](https://github.com/supercollider/sc3-plugins) extension is required, but the instructions for that are pretty simple and can be found on the project repository.
Once that's done, open the SuperCollider IDE and run the following code to use the [Quarks](http://doc.sccode.org/Guides/UsingQuarks.html) tool and install the atomiix quark.

`Quarks.install("https://github.com/rumblesan/atomiix.quark.git")`

To install the editor, first download and install [Atom](https://atom.io) and then the [atomiix](https://atom.io/packages/atomiix) package.


### Setup

By default, Atomiix will expect the default samples and letter mappings to be in the **~/atomiix/default** folder. The easiest way to set this up is to download the default-project file from the [releases](https://github.com/rumblesan/atomiix/releases) page and unzip it into your home directory.
It's also possible to change the default project directory by changing the settings in the Atom plugin.


### Custom Projects

There is also support for custom projects. If the _*.ixi_ file that you load in atom is in a folder containing a file called **atomiix.project** then Atomiix will check for a **samples** folder, a **keyMapping.yaml** file and a **synthdefs.scd** file and load these if they exist.


### Atom

It's possibly worth disabling the *bracket-matcher* plug-in in Atom so that it doesn't add in extra closing parentheses when changing the volume of an agent. This can be done from the Atom -> Preferences -> Packages menu.


## Running

To use Atomiix, start up the audio engine by running the following in the SuperCollider IDE.

`Atomiix.setup(57120, 57121);`

Create a file in Atom with the *.ixi* extension.

From the *Atomiix* sub menu in the *Packages* menu in Atom, click *Start Atomiix*.


## Key mappings

To evaluate code, any of the following key combinations can be used :-

* Ctrl-Enter
* Alt-Up
* Alt-Right

Alt-Left can be used to evaluate lines and free the agents on those lines.


## Differences from original Ixi lang

There are a number of differences between Atomiix and the original Ixi lang. Some of these are deliberate, some just haven't been implemented yet.

This list isn't exhaustive as there will likely be some differences that have been overlooked.

### Improved Editor Functionality

* Multiple lines can be evaluated at once. Just select them and run an evaluate command.

### Changes

* `>shift` and `<shift` are now `shiftr` and `shiftl` respectively.

### Missing

* All the tuning functionality (I don't understand how it works. Feel free to explain it to me)
* Agent specific scales
* The `sequence` command
* Meta-Agents
* The *intoxicant* commands
  - `hash`, `beer`, `coffee`, `LSD`, `detox`
* MIDI in/out
* snapshots
* `coder`, `autocode`, `matrix`
* `suicide` and `hotline`
* Score operators working as commands
* Auto-coder
* Recording sound file functionality


### Translations

Like Ixi lang, Atomiix supports translations of the language. Both in terms of the error and info messages displayed, and the language itself. Translations need to be added to the language and editor repositories currently, so please either open a pull-request with the changes, or get in contact so we can make it happen.


## TODO

Plenty! Not least more documentation and bug hunting. Please feel free to raise issues or send pull requests.


## Contact

Drop me an email at guy@rumblesan.com


## License

BSD License.
