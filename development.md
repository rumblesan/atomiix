# Developing

## Setup

Because the project is developed across three repositories, and has a few moving parts, development is a little tricky.
The following setup seems to work fairly painlessly though.

* Clone all the repositories
  - [Atomiix Language](https://github.com/rumblesan/atomiix)
  - [Atomiix Quark](https://github.com/rumblesan/atomiix.quark)
  - [Atomiix Editor](https://github.com/rumblesan/atomiix-editor)
* Make sure to have the following installed
  - Recent version of Node.js
  - SuperCollider
  - Atom Editor
    + Make sure that `apm`, the Atom Package Manager tool is available on the command line
* Link the main Atomiix language repository with the editor repository
  - In the main Atomiix repository run `npm link`
  - In the atomiix-editor repository, run `npm link @atomiix/atomiix`
  - This will mean that it shouldn't be necessary to keep running `npm install` in the editor repository
* Install the SuperCollider backend as a quark.
  - Running the following in the SuperCollider editor `Quarks.install(path/to/repo/atomiix.quark)`
  - If you're not planning to develop any of the SuperCollider code then it should also be possible to run `Quarks.install(https://github.com/rumblesan/atomiix.quark)`
* Start the SuperCollider backend
  - There is a script in the quark repository to do this (**scripts/run**) which assumes an OSX system
  - Alternatively, check the config in **scripts/startup.scd** and init the Atomiix class yourself
* In the atomiix-editor repository, run `apm link` to register the package folder with Atom

With all that done
* Startup the atom editor
* Create a new file with a *.ixi* extension
* Write some text e.g. `foo -> bass[1 2 3 4 ]`
* With your cursor on that line press *alt* and the *right arrow*

## Making changes

When making changes to the SuperCollider code, it should just be a matter of restarting SuperCollider and re-creating the Atomiix class again.

If making changes to the JavaScript client then it's necessary to rebuild the library by calling `npm run build` from within the **js** folder and then quitting and re-opening the Atom editor.

