# VS Code WPILib

[![CI](https://github.com/mccv/vscode-wpilib/actions/workflows/main.yml/badge.svg)](https://github.com/wpilibsuite/vscode-wpilib/actions/workflows/main.yml)

This repository contains a fork of the [WPILib VS Code extension](https://github.com/wpilibsuite/vscode-wpilib) updated to work in Cursor.

## Installing from a Release

If you want to install a pre-built version of the extension without building it yourself:

1. Go to the [Releases page](https://github.com/mccv/vscode-wpilib/releases)
2. Download the `.vsix` file from the latest release (found under the "WindowsVSIX" artifact)
3. In VS Code:
   - Open the Extensions view (Ctrl+Shift+X / Cmd+Shift+X)
   - Click the `...` menu at the top of the Extensions view
   - Select "Install from VSIX..."
   - Navigate to and select the downloaded `.vsix` file
4. Reload VS Code when prompted

The standalone utilities for Mac, Linux, and Windows are also available in each release.

## Build Dependencies

- Node JS - Tested with Node 18.
- Java - Tested with Java 17
- VS Code - For development/debugging.
  - TS Lint Extension
  - Chrome Debug Extension
  - In order to debug the extension, you will need the extension dependencies for the extension. The Microsoft C++ extension and the Java extension pack.

## Setting up Dependencies

In order to properly build, there is some setup that needs to occur.

1. Go into `vscode-wpilib` and run `npm install`
2. Go into into `wpilib-utility-standalone` and run `npm install`
3. From the root, run `./gradlew updateAllDependencies`. This will grab the templates and examples from WPILib, and move the shared dependencies from the vscode extension to the standalone utility. This command will need to be reran any time you update the shared dependencies in the vscode project.
4. Open the root folder in VS Code.

## Building and Debugging

Once you have the project open in VS Code, there are 5 debugging targets set up.

- `Extension` Will launch the extension to debug
- `Extension Tests` Will launch the extension tests
- `Standalone: Main` Will launch the standalone project. The debugger will be attached to the host process
- `Standalone: Renderer` Will attach to the standalone projects renderer process
- `Standalone: All` Will launch the standalone project, and attach to the renderer. This will attach 2 separate debuggers.

In addition, each project has a `compile` and a `lint` npm command. These will compile and lint their respective projects. Please run these before submitting any PR, as CI will check these. In addition, VS Code's lint does not detect the same lint errors as running lint manually would.

## Testing

We highly recommend you do any testing by launching in the debugger. For production use, install from a release (see above) rather than building locally.

## Warning about shared dependencies.

Because of limitiations in typescript, we cannot easily have a shared library that works in both the vscode extension and the standalone utility. Because VS Code is the primary platform, the files are stored in that folder. Anything in the following folder is considered shared.

- `vscode-wpilib/shared`
- `vscode-wpilib/riolog/shared`
  In these, any updates from the the standalone project will not be see in the vscode project, nor will they get committed to git. Please edit these files in the VS Code extension to apply changes.
