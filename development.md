# Developing

## Setup

Because the project is split across multiple repositories, and has a few moving parts, development is a little tricky.
The following set-up seems to work fairly painlessly though.

* Clone all the repositories
  - [Atomiix Language](https://github.com/rumblesan/atomiix-language)
  - [Atomiix Quark](https://github.com/rumblesan/atomiix.quark)
  - [Atomiix Editor](https://github.com/rumblesan/atomiix-editor)
* Make sure to have the following installed
  - Recent version of Node.js
  - SuperCollider
  - Atom Editor
    + Make sure that `apm`, the Atom Package Manager tool is available on the command line

If you're going to be developing the Atomiix language parser

* Link the main Atomiix language repository with the editor repository
  - In the atomiix-language repository run `npm link`
  - In the atomiix-editor repository, run `npm link @atomiix/atomiix`
    This will mean that when the editor loads the atomiix library it will pull it from the atomiix-language repository.
* Also in the atomiix-editor repository, run `apm link` to register the package folder with Atom
* Install the SuperCollider back end as a quark.
  - Running the following in the SuperCollider editor `Quarks.install(path/to/repo/atomiix.quark)`
  - If you're not planning to develop any of the SuperCollider code then it should also be possible to run `Quarks.install(https://github.com/rumblesan/atomiix.quark)`
* Start the SuperCollider back end
  - There is a script in the quark repository to do this (**scripts/run**) which assumes an OSX system
  - Alternatively, check the configuration in **scripts/startup.scd** and create the Atomiix class yourself

With all that done
* Start-up the Atomiix back end in SuperCollider.
  - Make sure you see the *Waiting for startup message* displayed.
* Start-up the atom editor.
* Create a new file with a *.ixi* extension.
* In the *Packages* menu, go to the *Atomiix* section and select *Start Atomiix*.
* Write some text e.g. `foo -> bass[1 2 3 4 ]`.
* With your cursor on that line press *Ctrl* and *Enter* together.

## Making changes

When making changes to the SuperCollider code, it should just be a matter of restarting SuperCollider and re-creating the Atomiix class again.

If making changes to the JavaScript client then it's necessary to rebuild the library by calling `npm run build` from within the **js** folder and then quitting and re-opening the Atom editor.

