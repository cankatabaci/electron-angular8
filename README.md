# Electron and Angular 8

Basic native desktop app with Electron and Angular 8

- Angular CLI: v8.2.1
- Node: v10.16.2
- Angular: v8.2.1
- Electron: v6.0.1

## Usage
```shell
git clone https://github.com/cankatabaci/electron-angular8.git
cd electron-angular8
npm install
npm run electron-build
```

## fine-tunings 

1- Fix Angular **src/index.html** (Add "." before slash) for electron

```html
<base href="./">
```

2- Create **main.js** for electron. In the main.js, as a start page, you should use in dist/index.html
```
const url = require('url')
const path = require('path')

win.loadURL(
    url.format({
      pathname: path.join(__dirname, "dist/index.html"),
      protocol:"file:",
      slashes: true
    })
  );
```

3- Edit **package.json**
```
"main": "main.js",
"scripts": {
    "electron": "electron .",
    "electron-build": "ng build --prod && electron ."
},
```

4- Edit **tsconfig.json** (edit _outDir_ and _target_)

I've solved the following error with the solution here
> Failed to load module script: The server responded with a non-JavaScript MIME type of "". Strict MIME type checking is enforced for module scripts per HTML spec.
```
"target": "es5",
```

5- Edit **angular.json** (Edit _outputPath_)
```
"outputPath": "dist",
```
