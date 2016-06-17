# NWJS Boilerplate

With Bootstrap 3 and JQuery.

## Getting started.
- [Install nwjs](http://nwjs.io/) if you haven't got it already.
- Install dependencies `npm install`
- `npm star` to kick start the app.

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

## `index.html`
Contains the nwjs "view" of the application. [Check it out](./index.html)
And has code for menu, and keyboards shortcut. Commented out ready for use.

## `main.js`
Optional if you want to run a node process in background. [more on this here](http://docs.nwjs.io/en/latest/References/Manifest%20Format/#node-main).

>`{String}` Specify the path to a node.js script file. And it will be executed on startup in Node context before the first DOM window load.

## Vendor folder
Contains Bootstrap and JQuery.

## Deploy

Use deploy script `deploy.js` by running folloring comand from root of app.

```
npm run build
```

This creates a build folder inside the repo. The build folder is also in `.gitignore` to avoid accidentally pushing it to remote.

[documentation on deployment](http://docs.nwjs.io/en/latest/For%20Users/Package%20and%20Distribute/)


## Other

- [NWJS documentaiton](http://docs.nwjs.io/en/latest/)
- [older documentation/wiki](https://github.com/nwjs/nw.js/wiki)
- [manifest format](http://docs.nwjs.io/en/latest/References/Manifest%20Format/#manifest-format)
- [NWJS contexts](http://docs.nwjs.io/en/latest/For%20Users/Advanced/JavaScript%20Contexts%20in%20NW.js/)
