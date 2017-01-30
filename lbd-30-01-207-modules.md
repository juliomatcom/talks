# Modules

## MODULE PURPOSES
### **What are JavaScript modules?** What is their purpose?
- Definition: how to encapsulate a piece of code into a useful unit, and how to register its capability/export a value for the module.
- Dependency References: how to refer to other units of code.   

http://requirejs.org/docs/whyamd.html#purposes  

### COMMONJS
https://webpack.github.io/docs/commonjs.html  

#### To achieve this CommonJS gives you two tools:

- the `require()` function, which allows to import a given module into the current scope.
- the `module` object, which allows you to export something from the current scope.

```javascript
/ salute.js
var MySalute = "Hello";
module.exports = MySalute;
```
```javascript
// world.js
var MySalute = require("./salute");
var Result = MySalute + "world!";
module.exports = Result;
```
### AMD

http://requirejs.org/docs/whyamd.html#amd

```javascript
define(['jquery'] , function ($) {
    return function () {};
});
```

#### It is an improvement over CommonJS modules because:   
It works better in the browser, it has the least amount of gotchas. Other approaches have problems with debugging, cross-domain/CDN usage, file:// usage and the need for server-specific tooling.  
Defines a way to include multiple modules in one file. In CommonJS terms, the term for this is a "transport format", and that group has not agreed on a transport format.   
Allows setting a function as the return value. This is really useful for constructor functions. In CommonJS this is more awkward, always having to set a property on the exports object. Node supports module.exports = function () {}, but that is not part of a CommonJS spec.  
