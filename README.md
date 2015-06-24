# bower.json specification


### name

**Required**  
Type: `String`

The name of the package as stored in the registry.

* Must be unique.
* Should be slug style for simplicity, consistency and compatibility. Example: `unicorn-cake`
* Lowercase, a-z, can contain digits, 0-9, can contain dash or dot but not start/end with them.
* Consecutive dashes or dots not allowed.
* 50 characters or less.


### description

*Recommended*  
Type: `String`

Any character. Max 140.

Help users identify and search for your package with a brief description. Describe what your package does, rather than what it's made of. Will be displayed in search/lookup results on the CLI and the website that can be used to search for packages.


### version

**Ignored by Bower as git tags are used instead.**

*Intended to be used in the future when Bower gets a real registry where you can publish actual packages, but for now just leave it out.*

<del>
Type: `String`

The package's semantic version number.

* Must be a [semantic version](http://semver.org) parseable by [node-semver](https://github.com/isaacs/node-semver).
* If publishing a folder, the version must be higher than the version stored in the registry, when republishing.
* Version should only be required if you are not using git tags.
</del>


### main

*Recommended*  
Type: `String` or `Array` of `String`

The entry-point files necessary to use your package. Only one file per filetype. The files that are offered should be representing your package as library. This means that the files can be used without compiling for use by the consuming party. This is not limited to **only** the 'compiled' version. In case of `.less`, `.scss` or `(d).ts` etc. they can be used as library as well when used in the consuming party source.

Entry-point files have module exports and may use module imports. While Bower does not directly use `main` files, they are listed with the commands `bower list --json` and `bower list --paths`, so they can be used by build tools.

Let's say your package looks like this:

    package
      js/
        motion.js
        run.js
        walk.js
      sass/
        motion.scss
        run.scss
        walk.scss
      img/
        motion.png
        walk.png
        run.png
      fonts/
        icons.woff2
        icons.woff
      dist/
        movement.js
        movement.min.js
        movement.css
        movement.min.css

`motion.js` has module imports for `run.js` and `walk.js`. `motion.scss` has module imports for `run.scss` and `walk.scss`. `main` would be

```
"main": [
  "js/motion.js",
  "sass/motion.scss",
  "dist/movement.css"
]
```

Image and font files may be used or referenced within the JS or Sass files, but are not `main` files as they are not entry-points.

* Use source files with module exports and imports over pre-built distribution files.
* Do not include minified files.
* Filenames should not be versioned (Bad: `package.1.1.0.js`; Good: `package.js`).
* Globs like `js/*.js` are not allowed.

### moduleType

Type: `String` or `Array` of `String`s

The type of module defined in the `main` JavaScript file. Can be one or an array of the following strings:

+ `globals`: JavaScript module that adds to global namespace, using `window.namespace` or `this.namespace` syntax
+ `amd`: JavaScript module compatible with AMD, like [RequireJS](http://requirejs.org/), using `define()` syntax
+ `node`: JavaScript module compatible with [node](https://nodejs.org/) and [CommonJS](https://nodejs.org/docs/latest/api/modules.html) using `module.exports` syntax
+ `es6`: JavaScript module compatible with [ECMAScript 6 modules](http://www.2ality.com/2014/09/es6-modules-final.html), using `export` and `import` syntax
+ `yui`: JavaScript module compatible with [YUI Modules](http://yuilibrary.com/yui/docs/yui/create.html), using `YUI.add()` syntax

### license

*Recommended*  
Type: `String` or `Array` of `String`

[SPDX license identifier](https://spdx.org/licenses/) or path/url to a license.


### ignore

*Recommended*  
Type: `Array` of `String`

A list of files for Bower to ignore when installing your package.

Note: symbolic links will always be ignored. However `bower.json` will never be ignored.

The ignore rules follow the same rules specified in the [gitignore pattern spec](http://git-scm.com/docs/gitignore).


### keywords

*Recommended*  
Type: `Array` of `String`

Same format requirements as [name](#name).

Used for search by keyword. Helps make your package easier to discover without people needing to know its name.


### authors

Type: `Array` of (`String` or `Object`)

A list of people that authored the contents of the package.

Either:

```json
"authors": [
  "John Doe", "John Doe <john@doe.com>",
  "John Doe <john@doe.com> (http://johndoe.com)"
]
```

or:

```json
"authors": [
  { "name": "John Doe" },
  { "name": "John Doe", "email": "john@doe.com" },
  { "name": "John Doe", "email": "john@doe.com", "homepage": "http://johndoe.com" }
]
```


### homepage

Type: `String`

URL to learn more about the package. Falls back to GitHub project if not specified and it’s a GitHub endpoint.


### repository

Type: `Object`

The repository in which the source code can be found.

```json
"repository": {
  "type": "git",
  "url": "git://github.com/foo/bar.git"
}
```


### dependencies

Type: `Object`

Dependencies are specified with a simple hash of package name to a semver compatible identifier or URL.

* Key must be a valid [name](#name).
* Value must be a valid [version](#version), a Git URL, or a URL (inc. tarball and zipball).
* Git URLs can be restricted to a reference (revision SHA, branch, or tag) by appending it after a hash, e.g. `https://github.com/owner/package.git#branch`.
* Value can be an owner/package shorthand, i.e. owner/package. By default, the shorthand resolves to GitHub -> git://github.com/{{owner}}/{{package}}.git. This may be changed in `.bowerrc` [shorthand_resolver](http://bower.io/docs/config/#shorthand-resolver).
* Local paths may be used as values for local development, but they will be disallowed when registering.


### devDependencies

Type: `Object`

Same rules as `dependencies`.

Dependencies that are only needed for development of the package, e.g., test framework or building documentation.


### resolutions

Type: `Object`

Dependency versions to automatically resolve with if conflicts occur between packages.

Example:

```json
"resolutions": {
  "angular": "1.3.0-beta.16"
}
```


### private

Type: `Boolean`

If you set it to `true` it will refuse to publish it. This is a way to prevent accidental publication of private repositories.
