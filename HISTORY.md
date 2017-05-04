## Revision history

### V1.3.8

* Added check to guard against catastrophic remote file deletion triggered by [this Meteor bug](https://github.com/vsivsi/meteor-file-collection/issues/152).
* Updated resumable.js to latest upstream version
* Removed jquery Atmosphere package as a dependency, as resumable.js no longer requires it.
* Documentation improvements

### V1.3.7

* Fixed server internal error when an HTTP requests matches the file-collection `baseURL` but does not match any of the defined HTTP interface definition paths. Also added unit test for this case. Thanks to @nathanbrizzee for reporting.
* Fixed (via gridfs-locking-stream npm package) an event memory leak when renewing locks on open files.
* Updated resumable.js to latest upstream version
* Updated npm and atmosphere dependencies for Meteor 1.4.2.3

### V1.3.6

* Fixed absolute URL for Cordova downloads. (thanks @crapthings)
* Updated npm and atmosphere dependencies for Meteor 1.3.4.4

### V1.3.5

* Added GET support for `Last-Modified-Since` HTTP header (thanks @edemaine)
* Fixed broken server tests when run on Windows (thanks @edemaine)
* Added `selector` parameter type check on function overriding default `remove` method (thanks @brucejo75)
* Updated Meteor package deps to 1.3.2.x versions
* Documentation updates for CORS, and cookie handling in sample code.

### V1.3.4

* Added `withCredentials: true` to the default Resumable object parameters to allow authentication with CORS
* Changed precedence of developer provided HTTP request handlers to come before default resumable.js route handlers, to permit adding headers to responses on that route.
* Updated resumable.js to latest `master`
* Updated npm dependencies.

### V1.3.3

* Use the internal MongoDB 2.1.x driver to create the indexes, not the Meteor provided 1.4.x driver, which is incompatible with MongoDB 3.2. Thanks to @snajjar for reporting.
* Updated package dependencies.

### v1.3.2

* Fixed bug when no HTTP options array is provided and resumable.js isn't used. Thanks to @ndarilek the PR.
* Updated npm dependencies.
* Documentation improvements.

### v1.3.1

* Fixed bugs affecting the built-in resumable.js support when application specified GET/POST routes also matched `/_resumable`. Fixes ensure that multipart parsing for POST requests only happens once, and that `_resumable` routes are fully handled before invoking application route handlers. Thanks to @lightpriest and @mzygmunt for reporting.

### v1.3.0

* Added ability to define custom HTTP OPTIONS request handlers, e.g. to support CORS
* The above feature can be used to add support for files in Apache Cordova apps. Thanks to @dnish for initial work on this.
* `maxUploadSize` option enables a configurable maximum file size for POST, PUT and resumable.js uploads. Thanks to @DanielDornhardt for this feature suggestion.
* Fixed improper ObjectID type in callback from `fc.upsertStream()`. Thanks @DrDanRyan for reporting.
* Updated to MongoDB 2.1.x driver
* Updated npm dependencies
* Added TravisCI support

### v1.2.2

* Fixed an uncaught throw in `importFile()` when the input file doesn't exist, thanks to @dpatte
* Updated resumable.js to latest master
* Updated dependencies
* Documentation improvements
* Fixed bug causing resumable HEAD requests to always return 404, even when a chunk was present in the gridFS store. Thanks to @dnish for help figuring this out.
* Fixed bug causing resumable GET requests to always return 204, even when a chunk was present in the gridFS store.
* Added unit tests for resumable.js GET/HEAD test request backend support
* Don't create unused readable streams for HTTP HEAD requests.
* Unit tests fixed for Meteor 1.2.x by adding many missing meteor packages to test build.

### v1.2.1

* This version number was accidentally skipped over, so there was no v1.2.1 release.

### v1.2.0

* Add the ability to perform limited local updates to the client minimongo collection using `fc.localUpdate()`
* Thanks to @Digital-Thor for his work on integrating [Sortable](https://github.com/RubaXa/Sortable/tree/master/meteor) and file-collection, demonstrating the usefulness of supporting local client-side update
* Fixed bug permitting `update` replacement of entire gridFS documents
* Added update related unit tests
* Defend against `Mongo.Collection !== Mongo.Collection.protype.constructor`
* Updated npm dependencies
* Updated resumable.js
* Switch to using HEAD requests for resumable.js chunk test requests
* Use `Meteor.Error` consistently

### v1.1.5

* Fixed issues related to lock timeouts and proper return values from `fc.remove()`
* Thanks to @timothyarmes for reporting these issues [issue 59](https://github.com/vsivsi/meteor-file-collection/issues/59)
* Added unit test coverage for basic `remove` functionality
* Documentation improvements
* Bumped npm dependencies
* Updated resumable.js to upstream master

### v1.1.4

* Resolving architecture specific build issues with newest mongodb driver

### v1.1.3

* Updated resumable.js and npm dependencies

### v1.1.2

* Checked in the `.versions` file
* Updated project directory structure, adding `src` and `test` subdirs.
* Updated npm dependencies.
* Documentation improvements.

### v1.1.1

* Added informative `throw` when server-only methods are erroneously called on the client
* Moved to current resumable.js master
* Bumped npm dependencies to latest versions
* Added explicit package version to `onTest()` call to work around a Meteor issue when running `meteor test-packages` within an app.
* Added ablity to set the resumable.js server side support MongoDB index name, via the `resumableIndexName` option to `new FileCollection()`. This fixes problems related to [issue 55](https://github.com/vsivsi/meteor-file-collection/issues/55). Thanks to @poojabansal for reporting.

### v1.1.0

* Changed the resumable.js server-side support to return status 204 for testChunk GET requests, rather than 404, which causes undesirable log entries in the client console.
* Fixed bug where received duplicate chunks could mistakenly both be written during resumable.js uploads
* Made POST body MIME/multipart parsing more resistent to malformed requests
* Added unit tests for resumable client and server-side support
* Automatic lock renewal support, can be controlled with `autoRenewLock` option on `fc.upsertStream()` and `fc.findOneStream()`
* `range` option to `fc.findOneStream()` now allows `start` or `end` to be safely omitted.
* Default `chunkSize` changed to 2MB - 1KB, matching the MongoDB recommendation for chunk sizes a little less than a power of 2.
* General performance improvements writing data to gridFS
* Updated mongodb, gridfs-locks and gridfs-locking-stream to newest versions

### v1.0.6

* Fixes #48, which caused unicode filenames to be corrupted in download SaveAs... dialogs. Thanks to @xurwxj for reporting.
* Bump versions of dependencies

### v1.0.5

* Version bump to enable publishing Windows platform build for Meteor 1.1

### v1.0.4

* Updated npm package dependencies

### v1.0.3

* Add automatic indexing for resumable.js queries, to improve uploading performance
* Bumped version of mongodb native driver

### v1.0.2

* Fixes failed unit test caused by null $set update query when using Meteor 1.0.4
* Update version of resumable.js
* Update mongodb npm package version
* Update meteor core package versions

### v1.0.1

* Fixes potential race condition in the underlying gridfs-locks package
* Updates npm package versions

### v1.0.0

* Added support for HTTP range requests (thanks to @riaan53!)
* Switched internally to using new style node.js streams for greatly improved flow-control when streaming large files
* HTTP access definitions may now include an optional custom express.js request handler function
* HTTP access file lookup functions may now access parsed MIME/multipart parameters for POST requests
* Updated all dependencies
* *BREAKING CHANGE:* `fc.upsertStream` may no longer append (mode 'w+') to existing files. This is a restriction added to the underlying node.js gridFS driver, and was a little used feature that was traded-off for node.js 0.10 new stream support

### v0.3.6

* Updated dependencies including resumable.js

### v0.3.5

* Rebuilt/published previous version using actual Meteor 1.0 instead of a checkout of Meteor 1.0

### v0.3.4

* Documentation improvements
* Dependent package version updates

### v0.3.3

* Added a polyfill for `Function.prototype.bind()` to enable compatibility with PhantomJS, which as of version 1.9.7 lacks support for `.bind()`
* Bumped mongodb npm package version.

### v0.3.2

* Bumped versions of npm dependencies, including a fix for a bson build error in the npm mongodb driver.

### v0.3.1

* Bumped versions of npm dependencies, including a fix for a rare gridfs file locking bug.
* Documentation fixes.

### v0.3.0

* Updated package name and information to conform with Meteor 0.9.0 package system. Thanks to @ryw for a PR that showed what needed to be done.
* Added versions.json file
* Documentation updates
* Added additional error checking when receiving a 'close' event.
* Don't automatically index the fileCollection.
* Updated express and mopngodb packages to latest versions
* All features deprecated in v0.2.0 are obsolete and removed

### v0.2.3

* Added additional checking that `_id` values in URLs are 24-digit hex strings before attempting to make them into ObjectIds
* Bumped express.js to latest version

### v0.2.2

* Fixed #15
* Updated README for new sample apps.
* Updated Resumable.js

### v0.2.1

* Added sanity checking of input to `fc.allow()` and `fc.deny()`
* Allow options to be truly optional w/ callback in `findOneStream()` and `upsertStream()`
* Fixed reversed/broken sort/skip options on `findOneStream()`
* Fixed an issue where `ObjectID`s in file metadata change type after `upsertStream()`
* Updated resumable.js
* Documentation improvements.

### v0.2.0

* `fc.allow` and `fc.deny` now support rules for the `'read'` operation, which secures HTTP GET/HEAD requests.
* `fc.allow` and `fc.deny` now support rules for the `'write'` operation, which impacts HTTP POST/PUT requests. `'write'` allow/deny rules are replacing the use of `'update'` rules, and work identically. The reason for the change is to avoid confusion with the `'update'` rules on Meteor collections and to better match the new `'read'` rules. `'update'` rules continue to work, but are now deprecated.
* HTTP GET requests now support the `?filename=somename.txt` query. This is similar to the `?download=true` option, except that the default filename used by the browser "Save As..." dialog is specified by the request URL.
* Added support for sending X-Auth-Token as an HTTP Cookie. This is safer than using the `?X-Auth-Token` URL query, which continues to work, but is now deprecated.
* When using the built-in Resumable.js upload support, if you create `'write'` allow/deny rules that depend on `userId` you must set an `X-Auth-Token` cookie. See the client [example code in README.md](https://github.com/vsivsi/meteor-file-collection#example) for an example of how to do this.
* Acceptance tests are now written in Coffeescript.
* Version updates for most Npm packages.
* Documentation improvements.
* The sample application has been moved to its own [GitHub repo](https://github.com/vsivsi/meteor-file-job-sample-app).
* Thanks to @elbowz for multiple feature suggestions.

### v0.1.18

* Allow/Deny rules are now called in the same order as in Meteor (deny rules go first).

### v0.1.17

* Fixed another issue when calling deprecated fileCollection object without new.

### v0.1.16

* Fixed issue when calling deprecated fileCollection object without new.

### v0.1.15

* Added FileCollection export
* Updated docs to use FileCollection and note that fileCollection is deprecated and will be removed in 0.2.0
* Added deprecation warning to console.warn for fileCollection use
* Bumped express version

### v0.1.14

* Improved documentation. Thanks to @renarl for suggestion.
* Updated express version.

### v0.1.13

* Updated versions of resumable, async, mongodb, gridfs-locks, gridfs-locking-stream and express
* Documentation improvements

### v0.1.12

* Fixed typos in documentation. Thanks to @dawjdh

### v0.1.11

* Fixed sample code in README.md. Thanks to @rcy

### v0.1.10

* Fixed resumable.js upload crash

### v0.1.9

* Fix missing filenames in resumable.js uploads caused by changes in mongodb 1.4.3
* upsertStream now correctly updates gridFS attributes when provided

### v0.1.8

* Updates for Meteor v0.8.1.1
* Documentation improvements
* Updated npm package versions

### v0.1.7

* Bumped package versions to fix more mongodb 2.4.x backwards compatility issues

### v0.1.6

* Bumped gridfs-locks version to fix a mongodb 2.4.x backwards compatility issue

### v0.1.0 - v0.1.5

* Initial revision and documentation improvements.
