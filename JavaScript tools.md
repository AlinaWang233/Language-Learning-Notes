# JavaScript package manager
To automate the process of downloading and upgrading JavaScript libraries from a central repository websites:
- 2013 Bower
- 2015 npm
- 2016 yarn(but it still uses npm packages under the hood)

## npm
Originally a package manager made specifically for node.js, a JavaScript runtime designed to run on the server, not the frontend
- Pro: we can now use npm to download and update our packages through the command line
- Con: digging through the node_modules folder to find the location of each package and manually including it in our HTML

### command
author, description, keywords, license, version

Dependencies: 
- SemVer : "package": "MAJOR.MINOR.PATCH"
- The MAJOR version should increment when you make **incompatible API changes**. 
- The MINOR version should increment when you **add functionality** in a backwards-compatible manner. 
- The PATCH version should increment when you make backwards-compatible **bug fixes**.
- Allow updates to any 1.2.x version of the package : `~1.2.13`
- Allow updates to any 1.x.x version of the package: `^1.2.13`


## Express
`app.listen(port)`:tells your server to listen on a given port, putting it in running state

`app.METHOD(PATH, HANDLER)`: Express routes
- METHOD is an http method in lowercase
- PATH is a relative path on the server (it can be a string, or even a regular expression)
- HANDLER is a function that Express calls when the route is matched. (ex. `function(req, res) {...}`)
ex. 
```JavaScript
app.get('/', function(req,res){
    res.send('Hello Express')
})
```

`res.sendFile(path)`: read & send files (html); can be put inside route HANDLER

absolute path = the Node global variable` __dirname` + relative path
 
`app.use(path, middlewareFunction)` : middleware(intercept route handlers, adding some kind of information)

`path`:optional. If you don’t pass it, the middleware will be executed for all requests.

`express.static(path)`: serve Static Assets(ex. other contents required by html)

`path`: the absolute path of the folder containing the static assets

REST API: allow data exchange without the need for clients to know any details about the server
(only need the resource URL and the action it wants to perform on the server)

JSON: a convenient data format to represent a JavaScript object as a string to be transmitted on the web

`.env`: a hidden file used to pass environment variables(API keys/database URI)
- shell file (no need to wrap names or values in quotes)
- cannot be space around the equal signs `VAR_NAME=value`

`process.env`: global Node object
`process.env.VAR_NAME`: access environment variables
- variabels passed as strings
- names all uppercase, words separated by an underscore



# JavaScript module bundler(webpack)
## Problem
JavaScript wasn’t originally designed with the feature of import code from one file to another, because JavaScript was designed to only run in the browser, with no access to the file system of the client’s computer (for security reasons) => load the file with the imported code first and then use it in another file

- 2009 CommonJS: specify an ecosystem for JavaScript to run outside the browser, add the feature above
- node.js: JavaScript runtime designed to run on the server, knowing all the npm paths to the modules

But it won't work for the browser because browser doesn't have access to the file system. Loading modules could be tricky: loading files dynamically, either synchronously (which **slows down execution**) or asynchronously (which can have **timing issues**).

## Solution: JavaScript module bundler
a tool that gets around the problem with a build step (which has access to the file system) to create a final output that is browser compatible (which doesn’t need access to the file system)

in this case, a tool to replace all the 'require' to be the actual content of the files => single bundled javascript file(with no require statements)
- 2011 browserify (node.js)
- 2015 webpack (React)

## Webpack
build method: `node_modules\.bin\webpack ./index.js --mode=development`
