# koop-github

[![Greenkeeper badge](https://badges.greenkeeper.io/koopjs/koop-provider-github.svg)](https://greenkeeper.io/)

> Github provider for [Koop](https://github.com/koopjs/koop)

[![npm][npm-image]][npm-url]
[![travis][travis-image]][travis-url]

[npm-image]: https://img.shields.io/npm/v/koop-github.svg?style=flat-square
[npm-url]: https://www.npmjs.com/package/koop-github
[travis-image]: https://travis-ci.org/koopjs/koop-provider-github.svg?branch=master
[travis-url]: https://travis-ci.org/koopjs/koop-provider-github

Take GeoJSON from a Github repository and serve it as an ArcGIS Feature Service, CSV, KML, or Shapefile.

## Install

Koop providers require that you first install Koop. For information on using Koop, see https://github.com/koopjs/koop.

You can add `koop-github` to your Koop server's dependencies by installing it with npm and adding it to your package.json like so:

```
npm install @koopjs/provider-github --save
```

## Usage

Make sure your koop configuration includes a github access token (`ghtoken` in the config object passed to koop or `KOOP_GITHUB_TOKEN` as an environmental variable). Your Github API requests will be rate limited and you will not have access private gists if you don't include a token.

```js
var koop = require('koop')({
  'ghtoken': 'XXXXXX' // defaults to `process.env.KOOP_GITHUB_TOKEN`
})
var koopGithub = require('@koopjs/provider-github')

koop.register(koopGithub)

koop.server.listen(1338, function () {
  console.log('Listening at http://%s:%d/', this.address().address, this.address().port)
})
```

Once `koop-github` is registered as provider and you've started your Koop server, you can request GeoJSON files in Github repositories using this pattern.  Note that the path within the repo uses `::` as a directory separator:

```
/github/{organization name}::{repository name}::{branch}::{folder::path::to::geojson}/FeatureServer/0/query
```

so for example:

```
http://localhost:1338/github/koopjs::geodata::master::countries::mexico/FeatureServer/0/query
```

## Test

`koop-github` uses [tape](https://github.com/substack/tape) for testing.

```
npm test
```

## Contributing

Esri welcomes contributions from anyone and everyone. Please see our [guidelines for contributing](https://github.com/Esri/contributing).

## License

[Apache 2.0](LICENSE)