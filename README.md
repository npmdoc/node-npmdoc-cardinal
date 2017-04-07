# api documentation for  [cardinal (v1.0.0)](https://github.com/thlorenz/cardinal#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-cardinal.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-cardinal) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-cardinal.svg)](https://travis-ci.org/npmdoc/node-npmdoc-cardinal)
#### Syntax highlights JavaScript code with ANSI colors to be printed to the terminal.

[![NPM](https://nodei.co/npm/cardinal.png?downloads=true)](https://www.npmjs.com/package/cardinal)

[![apidoc](https://npmdoc.github.io/node-npmdoc-cardinal/build/screenCapture.buildNpmdoc.browser.%2Fhome%2Ftravis%2Fbuild%2Fnpmdoc%2Fnode-npmdoc-cardinal%2Ftmp%2Fbuild%2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-cardinal/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-cardinal/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-cardinal/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Thorsten Lorenz",
        "email": "thlorenz@gmx.de",
        "url": "thlorenz.com"
    },
    "bin": {
        "cdl": "./bin/cdl.js"
    },
    "bugs": {
        "url": "https://github.com/thlorenz/cardinal/issues"
    },
    "dependencies": {
        "ansicolors": "~0.2.1",
        "redeyed": "~1.0.0"
    },
    "description": "Syntax highlights JavaScript code with ANSI colors to be printed to the terminal.",
    "devDependencies": {
        "readdirp": "~0.2.1",
        "tap": "~0.3.1"
    },
    "directories": {},
    "dist": {
        "shasum": "50e21c1b0aa37729f9377def196b5a9cec932ee9",
        "tarball": "https://registry.npmjs.org/cardinal/-/cardinal-1.0.0.tgz"
    },
    "gitHead": "ce0befef82535d86218fc32e5872809212e4b274",
    "homepage": "https://github.com/thlorenz/cardinal#readme",
    "keywords": [
        "syntax",
        "highlight",
        "theme",
        "javascript",
        "json",
        "terminal",
        "console",
        "print",
        "output"
    ],
    "license": "MIT",
    "main": "cardinal.js",
    "maintainers": [
        {
            "name": "thlorenz",
            "email": "thlorenz@gmx.de"
        }
    ],
    "name": "cardinal",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/thlorenz/cardinal.git"
    },
    "scripts": {
        "demo": "node examples/highlight-string.js; node examples/highlight-self; node examples/highlight-self-hide-semicolons;",
        "test": "tap ./test/*.js"
    },
    "version": "1.0.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module cardinal](#apidoc.module.cardinal)
1.  [function <span class="apidocSignatureSpan">cardinal.</span>highlight (code, opts)](#apidoc.element.cardinal.highlight)
1.  [function <span class="apidocSignatureSpan">cardinal.</span>highlightFile (fullPath, opts, cb)](#apidoc.element.cardinal.highlightFile)
1.  [function <span class="apidocSignatureSpan">cardinal.</span>highlightFileSync (fullPath, opts)](#apidoc.element.cardinal.highlightFileSync)
1.  object <span class="apidocSignatureSpan">cardinal.</span>settings
1.  object <span class="apidocSignatureSpan">cardinal.</span>utl

#### [module cardinal.settings](#apidoc.module.cardinal.settings)
1.  [function <span class="apidocSignatureSpan">cardinal.settings.</span>getSettings (home_)](#apidoc.element.cardinal.settings.getSettings)
1.  [function <span class="apidocSignatureSpan">cardinal.settings.</span>resolveTheme (home_)](#apidoc.element.cardinal.settings.resolveTheme)

#### [module cardinal.utl](#apidoc.module.cardinal.utl)
1.  [function <span class="apidocSignatureSpan">cardinal.utl.</span>inspect (obj, depth)](#apidoc.element.cardinal.utl.inspect)
1.  [function <span class="apidocSignatureSpan">cardinal.utl.</span>isPath (s)](#apidoc.element.cardinal.utl.isPath)



# <a name="apidoc.module.cardinal"></a>[module cardinal](#apidoc.module.cardinal)

#### <a name="apidoc.element.cardinal.highlight"></a>[function <span class="apidocSignatureSpan">cardinal.</span>highlight (code, opts)](#apidoc.element.cardinal.highlight)
- description and source-code
```javascript
function highlight(code, opts) {
  opts = opts || { };
  try {

    var result = redeyed(code, opts.theme || theme)
      , firstline = opts.firstline && !isNaN(opts.firstline) ? opts.firstline : 1;

    return opts.linenos ? addLinenos(result.code, firstline) : result.code;
  } catch (e) {
    e.message = 'Unable to perform highlight. The code contained syntax errors: ' + e.message;
    throw e;
  }
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.cardinal.highlightFile"></a>[function <span class="apidocSignatureSpan">cardinal.</span>highlightFile (fullPath, opts, cb)](#apidoc.element.cardinal.highlightFile)
- description and source-code
```javascript
function highlightFile(fullPath, opts, cb) {
  if (isFunction(opts)) {
    cb = opts;
    opts = { };
  }
  opts = opts || { };

  fs.readFile(fullPath, 'utf-8', function (err, code) {
    if (err) return cb(err);
    try {
      cb(null, highlight(code, opts));
    } catch (e) {
      cb(e);
    }
  });
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.cardinal.highlightFileSync"></a>[function <span class="apidocSignatureSpan">cardinal.</span>highlightFileSync (fullPath, opts)](#apidoc.element.cardinal.highlightFileSync)
- description and source-code
```javascript
function highlightFileSync(fullPath, opts) {
  var code = fs.readFileSync(fullPath, 'utf-8');
  opts = opts || { };
  return highlight(code, opts);
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.cardinal.settings"></a>[module cardinal.settings](#apidoc.module.cardinal.settings)

#### <a name="apidoc.element.cardinal.settings.getSettings"></a>[function <span class="apidocSignatureSpan">cardinal.settings.</span>getSettings (home_)](#apidoc.element.cardinal.settings.getSettings)
- description and source-code
```javascript
function getSettings(home_) {
  if (settings) return settings;
  try {
    settingsJson = fs.readFileSync(path.join(home_ || home, '.cardinalrc'), 'utf-8');
  } catch (_) {
    // no .cardinalrc found - not a problem
    return undefined;
  }
  try {
    return JSON.parse(settingsJson);
  } catch (e) {
    // Have a .cardinalrc, but something about it is wrong - warn the user
    // Coudn't parse the contained JSON
    console.error(e);
    return undefined;
  }
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.cardinal.settings.resolveTheme"></a>[function <span class="apidocSignatureSpan">cardinal.settings.</span>resolveTheme (home_)](#apidoc.element.cardinal.settings.resolveTheme)
- description and source-code
```javascript
function resolveTheme(home_) {
  var themePath
    , settings = getSettings(home_);

  if (!settings || !settings.theme) return undefined;

  try {
    // allow specifying just the name of a built-in theme or a full path to a custom theme
    themePath = utl.isPath(settings.theme) ? settings.theme : path.join(__dirname, 'themes', settings.theme);

    return require(themePath);
  } catch (e) {
    // Specified theme path is invalid
    console.error(e);
    return undefined;
  }
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.cardinal.utl"></a>[module cardinal.utl](#apidoc.module.cardinal.utl)

#### <a name="apidoc.element.cardinal.utl.inspect"></a>[function <span class="apidocSignatureSpan">cardinal.utl.</span>inspect (obj, depth)](#apidoc.element.cardinal.utl.inspect)
- description and source-code
```javascript
inspect = function (obj, depth) {
  console.log(util.inspect(obj, false, depth || 5, true));
}
```
- example usage
```shell
...
var util = require('util');

module.exports.isPath = function (s) {
  return (/[\/\\]/).test(s);
};

module.exports.inspect = function(obj, depth) {
  console.log(util.inspect(obj, false, depth || 5, true));
};
...
```

#### <a name="apidoc.element.cardinal.utl.isPath"></a>[function <span class="apidocSignatureSpan">cardinal.utl.</span>isPath (s)](#apidoc.element.cardinal.utl.isPath)
- description and source-code
```javascript
isPath = function (s) {
  return (/[\/\\]/).test(s);
}
```
- example usage
```shell
...
var themePath
  , settings = getSettings(home_);

if (!settings || !settings.theme) return undefined;

try {
  // allow specifying just the name of a built-in theme or a full path to a custom theme
  themePath = utl.isPath(settings.theme) ? settings.theme : path.join(__dirname, 'themes', settings.theme);

  return require(themePath);
} catch (e) {
  // Specified theme path is invalid
  console.error(e);
  return undefined;
}
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
