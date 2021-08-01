# protobufjs-for-appscript
This is a small helper library that helps us generate a single JS file of protobufjs for use in AppScript.

To do this yourself:

1. Install and build the library (you can give the global name anything you want.)

```console
npm install --save-dev protobufjs
npx esbuild index.js --bundle --global-name=psl --outfile=protobufjs.js
```

1. Copy the contents of protobuf.js to your AppScript (it will be called protobuf.gs, presumably) 

1. Use it

```javascript
const flightsProto = "my protofile as string"
const root = await psl.protobuf.parse(flightsProto).root
```

1. Note that you cannot load files so I converted my proto into a string.

1. You might also wish to test to see if you are running under AppScript so you can develop simulataneously locally and in AppScript. This piece of code might be useful.

```javascript
// Return true if this script is running under Google App Script
function underGoogleAppScript() {
  return typeof Utilities !== 'undefined' && Utilities.base64EncodeWebSafe !== 'undefined'
}
```

1. I use it like this:

```javascript
const protobuf = underGoogleAppScript() ? psl.protobuf : require("protobufjs");
const root = await protobuf.parse(flightsProto).root
```
