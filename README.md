Cloned from https://github.com/maphubs/tokml which was forked from https://github.com/mapbox/tokml

# tokml

Convert [GeoJSON](http://geojson.org/) to [KML](https://developers.google.com/kml/documentation/).

## Usage

with node/browserify

    npm install --save @maphubs/tokml

otherwise:

    wget https://raw.github.com/maphubs/tokml/master/tokml.js

as a binary:

    npm install -g @maphubs/tokml
    tokml file.geojson > file.kml
    tokml < file.geojson > file.kml
    

## Importing

ESM

```js
import * as tokml from "@maphubs/tokml"
```

CommonJS

```js
var tokml = require('@maphubs/tokml')
```

Browser

You can also load the built `tokml.js` file directly in a browser script tag and access it globally as `tokml()`


## Example

```js
// kml is a string of KML data, geojsonObject is a JavaScript object of
// GeoJSON data
var kml = tokml(geojsonObject);

// grab name and description properties from each object and write them in
// KML
var kmlNameDescription = tokml(geojsonObject, {
  name: "name",
  description: "description",
});

// name and describe the KML document as a whole
var kmlDocumentName = tokml(geojsonObject, {
  documentName: "My List Of Markers",
  documentDescription: "One of the many places you are not I am",
});
```

## API

### `tokml(geojsonObject, [options])`

Given [GeoJSON](http://geojson.org/) data as an object, return KML data as a
string of XML.

`options` is an optional object that takes the following options:

**The property to name/description mapping:** while GeoJSON supports freeform
`properties` on each feature, KML has an expectation of `name` and `description`
properties that are often styled and displayed automatically. These options let
you define a mapping from the GeoJSON style to KML's.

- `name`: the name of the property in each GeoJSON Feature that contains
  the feature's name
- `description`: the name of the property in each GeoJSON Feature that contains
  the feature's description

**Timestamp:** KML can associate features with a moment in time via the `TimeStamp` tag. GeoJSON doesn't
have a comparable field, but a custom property can be mapped

- `timestamp`: the name of the property in each GeoJSON Feature that contains
  a timestamp in XML Schema Time (yyyy-mm-ddThh:mm:sszzzzzz)

**Document name and description**: KML supports `name` and `description` properties
for the full document.

- `documentName`: the name of the full document
- `documentDescription`: the description of the full document

**[simplestyle-spec](https://github.com/mapbox/simplestyle-spec)** support:

- `simplestyle`: set to `true` to convert simplestyle-spec styles into KML styles

**Organic Map** style:

*  `organicMapsStyle`: set to `true` to use Organic Map styles. Use the `organicmaps-marker-color`and `organiorganicmaps-icon` properties. Valid values:
 - red
 - blue
 - purple
 - yellow
 - pink
 - brown
 - green
 - orange
 - deeppurple
 - lightblue
 - cyan
 - teal
 - lime
 - deeporange
 - gray
 - bluegray

## Development

Requires [node.js](http://nodejs.org/) and [browserify](https://github.com/substack/node-browserify):

To build `tokml.js`:

    make

To run tests:

    yarn install
    yarn run test
