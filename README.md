# api documentation for  [hasha (v2.2.0)](https://github.com/sindresorhus/hasha)  [![npm package](https://img.shields.io/npm/v/npmdoc-hasha.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-hasha) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-hasha.svg)](https://travis-ci.org/npmdoc/node-npmdoc-hasha)
#### Hashing made simple. Get the hash of a buffer/string/stream/file.

[![NPM](https://nodei.co/npm/hasha.png?downloads=true)](https://www.npmjs.com/package/hasha)

[![apidoc](https://npmdoc.github.io/node-npmdoc-hasha/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-hasha_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-hasha/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-hasha/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-hasha/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Sindre Sorhus",
        "email": "sindresorhus@gmail.com",
        "url": "sindresorhus.com"
    },
    "bugs": {
        "url": "https://github.com/sindresorhus/hasha/issues"
    },
    "dependencies": {
        "is-stream": "^1.0.1",
        "pinkie-promise": "^2.0.0"
    },
    "description": "Hashing made simple. Get the hash of a buffer/string/stream/file.",
    "devDependencies": {
        "ava": "*",
        "proxyquire": "^1.7.2",
        "xo": "*"
    },
    "directories": {},
    "dist": {
        "shasum": "78d7cbfc1e6d66303fe79837365984517b2f6ee1",
        "tarball": "https://registry.npmjs.org/hasha/-/hasha-2.2.0.tgz"
    },
    "engines": {
        "node": ">=0.10.0"
    },
    "files": [
        "index.js"
    ],
    "gitHead": "5104d62d41122047a9da143fcd05e9397ff494a2",
    "homepage": "https://github.com/sindresorhus/hasha",
    "keywords": [
        "hash",
        "hashing",
        "crypto",
        "hex",
        "base64",
        "md5",
        "sha1",
        "sha256",
        "sha512",
        "sum",
        "stream",
        "file",
        "fs",
        "buffer",
        "string",
        "text",
        "rev",
        "revving",
        "simple",
        "easy"
    ],
    "license": "MIT",
    "maintainers": [
        {
            "name": "sindresorhus",
            "email": "sindresorhus@gmail.com"
        }
    ],
    "name": "hasha",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/sindresorhus/hasha.git"
    },
    "scripts": {
        "test": "xo && ava"
    },
    "version": "2.2.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module hasha](#apidoc.module.hasha)
1.  [function <span class="apidocSignatureSpan">hasha.</span>fromFile (fp, opts)](#apidoc.element.hasha.fromFile)
1.  [function <span class="apidocSignatureSpan">hasha.</span>fromFileSync (fp, opts)](#apidoc.element.hasha.fromFileSync)
1.  [function <span class="apidocSignatureSpan">hasha.</span>fromStream (stream, opts)](#apidoc.element.hasha.fromStream)
1.  [function <span class="apidocSignatureSpan">hasha.</span>stream (opts)](#apidoc.element.hasha.stream)



# <a name="apidoc.module.hasha"></a>[module hasha](#apidoc.module.hasha)

#### <a name="apidoc.element.hasha.fromFile"></a>[function <span class="apidocSignatureSpan">hasha.</span>fromFile (fp, opts)](#apidoc.element.hasha.fromFile)
- description and source-code
```javascript
fromFile = function (fp, opts) {
	return hasha.fromStream(fs.createReadStream(fp), opts);
}
```
- example usage
```shell
...
process.stdin.pipe(hasha.stream()).pipe(process.stdout);
'''

'''js
var hasha = require('hasha');

// get the MD5 hash of an image
hasha.fromFile('unicorn.png', {algorithm: 'md5'}).then(function (hash) {
	console.log(hash);
	//=> '1abcb33beeb811dca15f0ac3e47b88d9'
});
'''


## API
...
```

#### <a name="apidoc.element.hasha.fromFileSync"></a>[function <span class="apidocSignatureSpan">hasha.</span>fromFileSync (fp, opts)](#apidoc.element.hasha.fromFileSync)
- description and source-code
```javascript
fromFileSync = function (fp, opts) {
	return hasha(fs.readFileSync(fp), opts);
}
```
- example usage
```shell
...

Returns a promise that resolves to a hash.

### hasha.fromFile(filepath, [options])

Returns a promise that resolves to a hash.

### hasha.fromFileSync(filepath, [options])

Returns a hash.


## Resources

- [Hasha: A Friendly Crypto API • DailyJS](http://dailyjs.com/2015/06/12/hasha-a-friendly-crypto-api/)
...
```

#### <a name="apidoc.element.hasha.fromStream"></a>[function <span class="apidocSignatureSpan">hasha.</span>fromStream (stream, opts)](#apidoc.element.hasha.fromStream)
- description and source-code
```javascript
fromStream = function (stream, opts) {
	if (!isStream(stream)) {
		return Promise.reject(new TypeError('Expected a stream'));
	}

	opts = opts || {};

	return new Promise(function (resolve, reject) {
		stream
			.on('error', reject)
			.pipe(hasha.stream(opts))
			.on('error', reject)
			.on('finish', function () {
				resolve(this.read());
			});
	});
}
```
- example usage
```shell
...
			.on('finish', function () {
				resolve(this.read());
			});
	});
};

hasha.fromFile = function (fp, opts) {
	return hasha.fromStream(fs.createReadStream(fp), opts);
};

hasha.fromFileSync = function (fp, opts) {
	return hasha(fs.readFileSync(fp), opts);
};
...
```

#### <a name="apidoc.element.hasha.stream"></a>[function <span class="apidocSignatureSpan">hasha.</span>stream (opts)](#apidoc.element.hasha.stream)
- description and source-code
```javascript
stream = function (opts) {
	opts = opts || {};

	var outputEncoding = opts.encoding || 'hex';

	if (outputEncoding === 'buffer') {
		outputEncoding = undefined;
	}

	var stream = crypto.createHash(opts.algorithm || 'sha512');
	stream.setEncoding(outputEncoding);
	return stream;
}
```
- example usage
```shell
...
	}

	opts = opts || {};

	return new Promise(function (resolve, reject) {
		stream
			.on('error', reject)
			.pipe(hasha.stream(opts))
			.on('error', reject)
			.on('finish', function () {
				resolve(this.read());
			});
	});
};
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
