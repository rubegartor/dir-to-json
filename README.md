# dir-to-json

> Asynchronously convert directory tree structure into a javascript object.

**Warning:** Only directories are listed in JSON object.
## Getting Started

package.json: 
```
"dir2Json": "https://github.com/rubegartor/dir-to-json.git",
```

Use in your project like this:

```javascript
var dirToJson = require('dir2Json');

dirToJson( "./path/to/my/dir", function( err, dirTree ){
	if( err ){
		throw err;
	}else{
		console.log( dirTree );
	}
});


// If you prefer, you can also use promises
dirToJson( "./path/to/my/dir" )
	.then( function( dirTree ){
		console.log( dirTree );
	})
	.catch( function( err ){
		throw err;
	});
```

## API

`dirToJson( path [, options ] [, callback ] )`

### path
* type: string
* description: Path to the directory you would like to obtain a tree object from.

### options *(optional)*
* type: object
* description: Allows output to be customized.
* Accepted properties:
	* **sortType** *boolean* (Default: `true`) - If `true`, directories will be listed before files in all `children` arrays. If `false`, array contents will be listed in the order which they are returned from `fs.readdir()`.

### callback( err, directoryTree ) *(optional)*
* type: function
* description: Callback function
	* err - Error object on fail. `null` on success.
	* directoryTree - Object containing heirarchical directory data.

## Structure of output

```javascript
{
	"parent": "..",
	"path": "",
	"text": "coverage",
	"children": [{
		"parent": "",
		"path": "coverage-final.json",
		"text": "coverage-final.json",
	}, {
		"parent": "",
		"path": "index.html",
		"text": "index.html",
	}, {
		"parent": "",
		"path": "lcov-report",
		"text": "lcov-report",
			"children": [{
			"parent": "lcov-report",
			"path": "lcov-report/index.html",
			"text": "index.html",
		}, {
			"parent": "lcov-report",
			"path": "lcov-report/prettify.css",
			"text": "prettify.css",
		}, {
			"parent": "lcov-report",
			"path": "lcov-report/prettify.js",
			"text": "prettify.js",
		}, {
			"parent": "lcov-report",
			"path": "lcov-report/src",
			"text": "src",
					"children": [{
				"parent": "lcov-report/src",
				"path": "lcov-report/src/createDirectoryObject.js.html",
				"text": "createDirectoryObject.js.html",
			}, {
				"parent": "lcov-report/src",
				"path": "lcov-report/src/index.html",
				"text": "index.html",
			}, {
				"parent": "lcov-report/src",
				"path": "lcov-report/src/main.js.html",
				"text": "main.js.html",
			}]
		}]
	}, {
		"parent": "",
		"path": "lcov.info",
		"text": "lcov.info",
	}, {
		"parent": "",
		"path": "prettify.css",
		"text": "prettify.css",
	}, {
		"parent": "",
		"path": "prettify.js",
		"text": "prettify.js",
	}, {
		"parent": "",
		"path": "src",
		"text": "src",
			"children": [{
			"parent": "src",
			"path": "src/createDirectoryObject.js.html",
			"text": "createDirectoryObject.js.html",
		}, {
			"parent": "src",
			"path": "src/index.html",
			"text": "index.html",
		}, {
			"parent": "src",
			"path": "src/main.js.html",
			"text": "main.js.html",
		}]
	}]
}
```