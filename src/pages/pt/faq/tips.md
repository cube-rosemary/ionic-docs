---
previousText: 'Security'
previousUrl: '/docs/faq/security'
contributors:
  - rtpHarry
  - FdezRomero
  - brandyscarney
---

# Developer Tips

## Resolving Permission Errors

`EACCES` permission errors can occur when packages are installed globally. If this is the case, npm may need to be set up to operate without elevated permissions.

> Using `sudo` with npm is **not recommended** because it can lead to further complications.

This guide offers two options for resolving permission issues. See the [npm docs](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally) for full documentation and additional options.

### Option 1

The best way to avoid permission issues is to reinstall NodeJS and npm using a node version manager.

This guide will document [nvm](https://github.com/nvm-sh/nvm) installation and usage. See the [nvm docs](https://github.com/nvm-sh/nvm#installation-and-update) for full documentation. See the [npm docs](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm#using-a-node-version-manager-to-install-nodejs-and-npm) for additional options and instructions for Windows.

1. Install nvm.

    ```shell
    $ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
    ```

1. New terminals will now use nvm. To verify, open a new terminal and run the following. If something prints, the installation was successful.

    ```shell
    $ command -v nvm
    ```

1. To download and install the latest LTS release of NodeJS, run:

    ```shell
    $ nvm install --lts
    ```

1. Set the newly installed NodeJS as the default environment:

    ```shell
    $ nvm alias default lts/*
    ```

1. New terminals will now use the nvm-controlled NodeJS. To verify:

    ```shell
    $ node -v  # will print the version installed above
    $ which npm  # will print a path somewhere within the ~/.nvm folder
    ```

Global packages will now be installed in the `~/.nvm` directory, so permission errors should no longer occur as long as `npm` is used *without* `sudo`.

### Option 2

<small><em>Does not apply to Windows</em></small>

Change the owner of npm's directories to the current user:

```shell
$ sudo chown -R $(whoami) /usr/local/{lib/node_modules,bin,share}
$ sudo chown -R $(whoami) ~/.npm ~/.npmrc
```

Since these global directories are no longer owned by `root`, packages can be installed globally *without* `sudo`.

## Updating Dependencies

To update an [npm](https://www.npmjs.com/) dependency, run the following, where `<package-name>` is the package to update:

```shell
$ npm install <package-name>@<version|latest> --save
```

For example, to update the `@ionic/angular` package to the release tagged `latest`, run:

```shell
$ npm install @ionic/angular@latest --save
```

It is recommended that packages get updated through the CLI since npm will now read package versions from the `package-lock.json` first.

## Editors

There are a lots of editors to choose from. Here are some of our favorites:

- [Ionic Studio](https://ionicframework.com/studio?utm_source=docs&utm_medium=website&utm_campaign=studio%20launch): the fastest and easiest way to build Ionic apps
- [VS Code](https://code.visualstudio.com): a popular and free text editor made by Microsoft
- [Atom](https://atom.io): a hackable text editor made by GitHub
- [WebStorm](https://www.jetbrains.com/webstorm/): a powerful non-free editor by JetBrains

## Using a Debugger

The `debugger` keyword can be used to debug an app. When most browsers encounters a `debugger` statement, running of JavaScript is stopped, and the browser will load its debugger. This can be used to set "breakpoints" in the app.

For example, if a function is not returning the correct value, the debugger can be used to step through the code and inspect variables.

```javascript
function myBrokenFunction() {
  debugger;
  // do other stuff
}
```

When an app runs, it will pause at this function. From there, the developer tools can be used to run pieces of JavaScript, line by line, and inspect where exactly the function breaks.

## Changing Mode

By default, when an app is viewed in the browser, Ionic will apply the `md` mode. However, since Ionic components adapt according to their platform, it is helpful to be able to view what this app looks like on iOS. To do this, add `?ionic:mode=ios` to the URL where the app is being served: `http://localhost:8100/?ionic:mode=ios`.

> However, this will not change how the browser sees which platform is currently being used. Platform is determined by device detection and inspecting the user-agent. So to change the platform, the user-agent must be changed. To do this, open up Chrome DevTools with <kbd>Ctrl+Shift+I</kbd>(<kbd>Cmd+Option+I</kbd> on Mac), and then toggle device mode on with <kbd>Ctrl+Shift+M</kbd>(<kbd>Cmd+Option+M</kbd> on Mac).

![app with a different mode](/docs/v4/assets/img/faq/tips/change-device-platform.png)

Selecting devices from the device dropdown will change the user-agent, as well as the dimensions of the viewport.

## Using the iOS Simulator

The iOS simulator enables testing and debugging of an app before it reaches an actual device.

Before it can be used, [Xcode](https://developer.apple.com/xcode/download/), Apple's IDE, must be installed.

The [Ionic CLI](/docs/cli) can then be used to run the app in the current directory on the simulator:

```shell
$ ionic cordova emulate ios -lc
```

Passing in the `-lc` flag will enable livereload and log console output to a terminal.

Xcode can also be used to launch the emulator and debug an app.

Open up Xcode and open `../path-to-app/platforms/ios/myApp.xcodeproj`.

After the app loads, console output and device logs will be printed inside of Xcode's output window.

## Using the Genymotion Android Emulator

While the Android SDK comes with a stock emulator, it can be slow and unresponsive at times.

[Genymotion](https://www.genymotion.com) is an alternate emulator that is faster, and still allows access to native functionality like GPS and camera.

## Remote Debugging - iOS and Safari

Safari can be used to debug an Ionic app on a connected iOS device.

First, Web Inspector needs to be enabled on the connected device.

Web Inspector can be found under `Settings > Safari > Advanced`.

Next, head over to the Safari on a Mac and enable **Show Develop menu in menu bar** under `Safari > Preferences > Advanced`.

The connected device should now appear in the **Develop** menu.

From there, Safari's developer tools can be used to inspect and debug the app.

## Remote Debugging - Android and Chrome

Chrome DevTools can be used to debug an app when it is running in the browser through `ionic serve`, deployed to an emulator, or a physical device.

To inspect an emulator or physical device, go to `chrome://inspect/#devices` in Chrome, and select the remote target which has the running app.

> Note: Physical devices might need to have developer mode enabled in order to debug from Chrome.

## Remote Debugging - VS Code Plugin

VS Code has a dedicated plugin for debugging apps built with Cordova.

[The plugin](https://marketplace.visualstudio.com/items?itemName=vsmobile.cordova-tools) creates a bridge between the device and the VS Code Devtools and allows debugging to be done right in the editor.