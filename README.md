# bower.json specification


### name

**Required**  
Type: `String`

The name of the package as stored in the registry.

* Must be unique.
* Should be slug style for simplicity, consistency and compatibility. Example: `unicorn-cake`
* Lowercase, a-z, can contain dash or dot but not start/end with them.
* Consecutive dashes or dots not allowed.
* 50 characters or less.


### description

*Recommended*  
Type: `String`

Any character. Max 140.

Help users identify and search for your package with a brief description. Describe what your package does, rather than what it's made of. Will be displayed in search/lookup results on the CLI and the website that can be used to search for packages.


### version

Type: `String`

The package's semantic version number.

* Must be a [semantic version](http://semver.org) parseable by [node-semver](https://github.com/isaacs/node-semver).
* If publishing a folder, the version must be higher than the version stored in the registry, when republishing.
* Version should only be required if you are not using git tags.


### main

*Recommended*  
Type: `String` or `Array` of `String`

The primary acting files necessary to use your package. While Bower does not directly use these files, they are listed with the commands `bower list --json` and `bower list --paths`, so they can be used by build tools.

* Preprocessor files like CoffeeScript should be compiled.
* Do not include minified files.
* Filenames should not be versioned (Bad: package.1.1.0.js; Good: package.js).


### license

*Recommended*  
Type: `String` or `Array` of `String`

[SPDX license identifier](https://spdx.org/licenses/) or path/url to a license.


### ignore

*Recommended*  
Type: `Array` of `String`

A list of files for Bower to ignore when installing your package.

Note: README (all variants of case, .md, .text) and bower.json will never be ignored.

The ignore rules follow the same rules specified in the [gitignore pattern spec](http://git-scm.com/docs/gitignore).


### keywords

*Recommended*  
Type: `Array` of `String`

Same format requirements as [name](#name).

Used for search by keyword. Helps make your package easier to discover without people needing to know its name. Recommended.


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
  { "name": "John Doe", "email": "john@doe.com"," homepage": "http://johndoe.com" }
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
* Value can be an owner/package shorthand, i.e. owner/package. By default, the shorthand resolves to GitHub -> https://github.com/owner/package. This may be changed in `.bowerrc` shorthand_resolver.
* Local paths may be used as values for local development, but they will be disallowed when registering.


### devDependencies

Type: `Object`

Same rules as `dependencies`.

Dependencies that are only needed for development of the package, e.g., test framework or building documentation.


### resolutions

Type: `Object`

Dependency versions to automatically resolve with if conflicts occur between packages.


### private

Type: `Boolean`

If you set it to `true` it will refuse to publish it. This is a way to prevent accidental publication of private repositories.
