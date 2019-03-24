# Atomiix

Atomiix is a re-implementation of the Ixilang live-coding environment.

The documentation already assumes some knowledge of Ixilang, and needs to be greatly improved.

There are also bugs, though this is just about at the stage where it's usable and hopefully useful.


## Installation

Atomiix has two parts, the audio engine written in SuperCollider and the Atom editor plugin.

Installing SuperCollider should just involve going to the [Download](https://supercollider.github.io/download) page on the website, downloading the most recent version for your platform, and then running the installer.
Once that's done, open the SuperCollider IDE and run the following code to use the [Quarks](http://doc.sccode.org/Guides/UsingQuarks.html) tool and install the atomiix quark.

`Quarks.install("https://github.com/rumblesan/atomiix.quark.git")`

To install the editor, first download and install [Atom](https://atom.io) and then the [atomiix](https://atom.io/packages/atomiix) package.

### Setup

By default, Atomiix will expect the default samples and letter mappings to be in the **~/atomiix/default** folder. The easiest way to set this up is to download the default-project file from the [releases](https://github.com/rumblesan/atomiix/releases) page and unzip it into your home directory.
It's also possible to change the default project directory by changing the settings in the Atom plugin.

### Custom Projects

There is also support for custom projects. If the _*.ixi_ file that you load in atom is in a folder containing a file called **atomiix.project** then Atomiix will check for a **samples** folder, a **keyMapping.ixi** file and a **synthdefs.scd** file and load these if they exist.


## Running

To use Atomiix, start up the audio engine by running the following in the SuperCollider IDE

`Atomiix.setup(57120, 57121);`

Create a file in Atom with the *.ixi* extension.

From the *Atomiix* sub menu from the *Packages* menu in Atom, then click *Start Atomiix*.


## Key mappings

To evaluate code, any of the following key combinations can be used :-

* Alt-Up
* Alt-Right
* Ctrl-Enter

Alt-Left can be used to evaluate lines and free the agents on those lines.


## Differences from original Ixilang

There are a number of differences between Atomiix and the original Ixilang. Some of these are deliberate, some just haven't been implemented yet.

This list isn't exhaustive as there will likely be some differences that have been overlooked.

### Improved Functionality

* Multiple lines can be evaluated at once. Just select them and run an evaluate command.

### Changes

* `>shift` and `<shift` are now `shiftr` and `shiftl` respectively.

### Missing

* All the tuning functionality (I don't understand how it works. Feel free to explain it to me)
* Agent specific scales
* Score sequencing
* Plenty of commands
  - `swap`, `replace`, `insert`, `remove`, `invert`, `order`, `hash`, `beer`, `coffee`, `LSD`, `detox`
* MIDI in/out
* snapshots
* `coder`, `autocode`, `matrix`
* `suicide` and `hotline`
* Chords in melodic scores
* Score operators working as commands


## TODO

Plenty! Not least more documentation and bug hunting. Please feel free to raise issues or send pull requests.


## Contact

Drop me an email at guy@rumblesan.com


## License

BSD License.

