# Deploying

*To sign on Mac, you need a developer account and a distribution certificate. Electron-build will auto pick up the cert if it exists*  

Way2 may be easy for private repos too

## Way 1: AutoUpdate Server

### Hazel

Easy zeit creation that pulls from github releases even for **private repos**

```bash
git clone https://github.com/zeit/hazel
cd hazel

#PUBLIC REPOS
now -e ACCOUNT="<github-account>" -e REPOSITORY="<github-repository>"
#Private REPOS
now --prod -e URL='https://<NOW DOMAIN>.now.sh' -e TOKEN="<GITHUB_TOKEN>" -e ACCOUNT="jsfuentes" -e REPOSITORY="Room"
```

**Only run in the prod app version**

```js
const { app, autoUpdater } = require('electron')

const server = <your-deployment-url>
const feed = `${server}/update/${process.platform}/${app.getVersion()}`

autoUpdater.setFeedURL(feed)

setInterval(() => {
  autoUpdater.checkForUpdates()
}, 600000) //check every 10 minutes
```

Notifying user

```js
autoUpdater.on('update-downloaded', (event, releaseNotes, releaseName) => {
  const dialogOpts = {
    type: 'info',
    buttons: ['Restart', 'Later'],
    title: 'Application Update',
    message: process.platform === 'win32' ? releaseNotes : releaseName,
    detail: 'A new version has been downloaded. Restart the application to apply the updates.'
  }

  dialog.showMessageBox(dialogOpts).then((returnValue) => {
    if (returnValue.response === 0) autoUpdater.quitAndInstall()
  })
})

autoUpdater.on('error', message => {
  console.error('There was a problem updating the application')
  console.error(message)
})
```

## Way 2: Electron-Updater

Easiest setup! Struggles with private repos, apparently private repos work here too

1)

```bash
npm install electron-updater
```

2) [Configure publish](https://www.electron.build/configuration/publish) in package.json under "build" key

3)  

```js
const { autoUpdater } = require("electron-updater")

export default class AppUpdater {
  constructor() {
    const log = require("electron-log");
    log.transports.file.level = "info";
    autoUpdater.logger = log;
    autoUpdater.checkForUpdatesAndNotify();
  }
}

//...createMainWindow function {
	new AppUpdater();
}
```

#### Electron-updater Vs. built-in autoUpdater

- Dedicated release server is not required.
- Code signature validation on mac & win
- All required metadata auto produced & published
- Download progress and [staged rollouts](https://www.electron.build/auto-update#staged-rollouts) supported on all platforms.
- Different providers supported out of the box ([GitHub Releases](https://help.github.com/articles/about-releases/), [Amazon S3](https://aws.amazon.com/s3/), [DigitalOcean Spaces](https://www.digitalocean.com/community/tutorials/an-introduction-to-digitalocean-spaces), [Bintray](https://bintray.com/) and generic HTTP(s) server).
- You need only 2 lines of code to make it work.

https://github.com/electron/electron/issues/7155)

## Way 3, Electron Way: 

Electron team maintains free [update.electronjs.org](https://github.com/electron/update.electronjs.org) for free apps in github releases

- App runs on macOS or Windows
- App has a public GitHub repository
- Builds are published to GitHub Releases
- Builds are code-signed

**On Mac:** App must be [signed](https://www.electron.build/code-signing) for auto updates, based on  [Squirrel.Mac](https://github.com/Squirrel/Squirrel.Mac)

**On WIndows:** Make sure not to update app the [first time it runs](****