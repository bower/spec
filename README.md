# Bower spec

`bower.json` - The package manifest

---

**name (required) [string]**

The name of the package as stored in the registry.

* Should be slug style for simplicity, consistency and compatibility.
* Must be unique
* Lowercase, a-z, can contain dash or dot but not start/end with them.
* Consecutive dashes or dots not allowed

---

**version [string]**

The current version of the package.

* Must be a semantic version - http://semver.org/ - i.e, parseable by [node-semver.](https://github.com/isaacs/node-semver)
* If publishing a folder, the version must be higher than the version stored in the registry, when republishing.
* Version should only be required if you are not using Git tags.

---

**location [string]**

The endpoint where Bower can find your package. This is used during registration.

---

**description [string]**

Help users identify and search for your package with a brief description. Describe what your package does, rather than what it's made of. Will be displayed in search/lookup results on the CLI and the website that can be used to search for packages. Recommended.

* Any character. Max 140.

---

**keywords [array of strings]**

Used for search by keyword. Helps make your package easier to discover without people needing to know its name. Recommended.

* Same format requirements as `name`.

---

**main [string|array of strings]**

The primary acting files necessary to use your package. While Bower does not directly use these files, they are listed with the commands `bower list --json` and `bower list --paths`, so they can be used by build tools.

* Coffeescript should be compiled.
* Do not include minified files.
* Files should not be versioned (Bad: package.1.1.0.js; Good: package.js).


---

**dependencies [hash]**

Dependencies are specified with a simple hash of package name to a semver compatible identifier or URL.

* Key must be a <name> that matches the validation pattern for the `name` property.
* Value must be a semver compatible identifier, a Git URL, or a URL (inc. tarball and zipball).
* Value can be an owner/package shorthand, i.e. owner/package. By default, the shorthand resolves to GitHub -> https://github.com/owner/package. This may be changed in .bowerrc shorthand_resolver.
* Local paths may be used as values for local development. But they will be disallowed when registering.

---

**devDependencies [hash]**

Dependencies that are only needed for development of the package, e.g., test framework or building documentation.

---

**ignore [array of strings]**

A list of files for Bower to ignore when installing your package. Note: README (all variants of case, .md, .text) will never be ignored.

* The ignore rules follow the same rules specified in the gitignore pattern spec.

---

**license [string | array of strings]**

[SPDX license identifier](https://spdx.org/licenses/) or path/url to license.

---

**authors [array of strings|array of hashes]**

Either `”authors”: [“John Doe”, “John Doe <john@doe.com>”, “John Doe <john@doe.com> (http://johndoe.com)”]`
or: `”authors”: [{ “name”: “John Doe” }, { “name”: “John Doe”, “email”: “john@doe.com” },  { “name”: “John Doe”, “email”: “john@doe.com”,” homepage”: “http://johndoe.com” }]`

---

**homepage [string]**

URL to learn more about the package. Falls back to GitHub project if not specified and it’s a GitHub endpoint.

---

**repository [object]**

The repository in which the source code can be found.

`”repository: { “type”: “git”, “url”: “git://github.com/foo/bar.git” }”`

---

**private [string boolean]**

If you set `"private": true` in your bower.json, it will refuse to publish it. This is a way to prevent accidental publication of private repositories.