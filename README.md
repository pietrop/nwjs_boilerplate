# NWJS Boilerplate

A simple NWJS boilerplate to get started prototyping apps for os x with node. jQuery and Bootstrap 3.

## Getting started.
- [Install nwjs](http://nwjs.io/) if you haven't got it already.
- Install dependencies `npm install`
- `npm star` to kick start the app.

If you don't want to install nwjs globally on your system you can try and add this to `package.json` as a dev dependency and see how if it works.

```javascript
"devDependencies": {
  "nw": "^0.15.2"
}
```

## How to use it
At is simplest, go into `index.html` make a script tag, write your javascript in there, and require any node module you need (after having npm installed them locally)

Check out the [NWJS documentaiton](http://docs.nwjs.io/en/latest/) for more on how to do things with NWJS.

You may want to have a look at [NWJS contexts](http://docs.nwjs.io/en/latest/For%20Users/Advanced/JavaScript%20Contexts%20in%20NW.js/) for a better understanding of the thin line between the dom and node in NWJS.

## Overview

```
.
├── README.md
├── deploy.js
├── index.html
├── main.js
├── node_modules
|   └── ...
├── package.json
└── vendor
    ├── bootstrap-3.3.6-dist
    │   ├── css
    │   │   ├── bootstrap-theme.css
    │   │   ├── bootstrap-theme.css.map
    │   │   ├── bootstrap-theme.min.css
    │   │   ├── bootstrap-theme.min.css.map
    │   │   ├── bootstrap.css
    │   │   ├── bootstrap.css.map
    │   │   ├── bootstrap.min.css
    │   │   └── bootstrap.min.css.map
    │   ├── fonts
    │   │   ├── glyphicons-halflings-regular.eot
    │   │   ├── glyphicons-halflings-regular.svg
    │   │   ├── glyphicons-halflings-regular.ttf
    │   │   ├── glyphicons-halflings-regular.woff
    │   │   └── glyphicons-halflings-regular.woff2
    │   └── js
    │       ├── bootstrap.js
    │       ├── bootstrap.min.js
    │       └── npm.js
    └── jquery.min.js
```

## `Package.json`

```json
{
  "name": "nwjs_boilerplate",
  "version": "1.0.0",
  "description": "a sample Boilerplate to get started with nwjs applications",
  "main": "index.html",
  "node-main": "main.js",
  "dom_storage_quota": 5,
  "window": {
    "show": true,
    "frame": true,
    "toolbar": true,
    "always_on_top": true,
    "fullscreen": false,
    "show_in_taskbar": true,
    "transparent": false,
    "icon": "app.icns",
    "width": 800,
    "height": 500,
    "position": "mouse",
    "min_width": 400,
    "min_height": 200,
    "max_width": 800,
    "max_height": 600
  },
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "nw",
    "build": "node deploy.js",
    "testing": "echo hello"
  },
  "author": "Pietro Passarelli <pietro.passarelli@gmail.com> (http://pietropassarelli.com)",
  "license": "ISC",
  "dependencies": {
    "nw-builder": "^2.2.0"
  }
}
```

[`"dom_storage_quota"`](http://docs.nwjs.io/en/latest/References/Manifest%20Format/#dom_storage_quota) is the size of local storage you have access to within NWJS. meausered in MB by default in browsers is a round 5mb.

## `index.html`
Contains the nwjs "view" of the application. [Check it out](./index.html)
It has code for menu, and keyboards shortcut. Commented out ready for use.

## `main.js`
Optional if you want to run a node process in background. [more on this here](http://docs.nwjs.io/en/latest/References/Manifest%20Format/#node-main).

>`{String}` Specify the path to a node.js script file. And it will be executed on startup in Node context before the first DOM window load.

## Vendor folder
Contains Bootstrap and JQuery.

## Deploy

Use deploy script `deploy.js` by running following comand from root of app.

```
npm run build
```

This creates a build folder inside the repo. The build folder is also in `.gitignore` to avoid accidentally pushing it to remote.

[documentation on deployment](http://docs.nwjs.io/en/latest/For%20Users/Package%20and%20Distribute/)

Also note that

>The first item of application menu shows nwjs instead of your-app-name. To fix it, you need to set the value of CFBundleName in all files of `nwjs.app/Contents/Resources/*.lproj/InfoPlist.strings` to `your-app-name` instead of nwjs.

Before running the deploy script you may also want to change toolbar show option to false, in `package.json`. I have it on by default because is useful for troubleshooting during development.

```json
"toolbar": false,
```

## Debugging

by default I've added `nw --remote-debugging-port=9222` in the `package.json` `start` script, for easy debugging.

[checkout the documentation for more on this](http://docs.nwjs.io/en/latest/For%20Users/Debugging%20with%20DevTools/)

To disabled this change start script to `nw` only.


to use it run the app with `npm start` and visit [http://localhost:9222/](http://localhost:9222/) there you can chose the app you are currently working on, and it will show you the inspector in the browser.


## local modules path

After considering [a bunch of different options](https://gist.github.com/branneman/8048520)

Decided to go for the [app-module-path](https://www.npmjs.com/package/app-module-path) as it seemed to be the most straightforward.

To use it in nwjs you need to do a little tweak due to the [difference in js context between node and webkit, install it](https://github.com/nwjs/nw.js/wiki/Differences-of-JavaScript-contexts).

```
npm install app-module-path --save
```

in `index.html` instead of using the recomended `__dirname`  

```js
require('app-module-path').addPath(__dirname);
```

replace that with `"."`


```js
require('app-module-path').addPath(".");
```
and it will work as normal.

eg a module deep in the folder structure, can require another model just using the path from the root of the application, rather then having to work out some relative path that gets very confusing very quickly..

```js
var Transcription = require('app/models/transcription');
```

I did not put this in the `package.json` coz different people/projects have different ways of doing(or not doing) this. But now you know how to add it if you wish to use it.

## Other

- [NWJS documentaiton](http://docs.nwjs.io/en/latest/)
- [older documentation/wiki](https://github.com/nwjs/nw.js/wiki)
- [manifest format](http://docs.nwjs.io/en/latest/References/Manifest%20Format/#manifest-format)
- [NWJS contexts](http://docs.nwjs.io/en/latest/For%20Users/Advanced/JavaScript%20Contexts%20in%20NW.js/)
- [Sample NWJS Apps](https://github.com/zcbenz/nw-sample-apps)
