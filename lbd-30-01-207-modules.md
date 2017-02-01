# Modules

### MODULE PURPOSES
### **What are JavaScript modules?** What is their purpose?
- Definition: how to encapsulate a piece of code into a useful unit, and how to register its capability/export a value for the module.
- Dependency References: how to refer to other units of code.   

http://requirejs.org/docs/whyamd.html#purposes  

### COMMONJS
https://webpack.github.io/docs/commonjs.html  

- Compact syntax
- Designed for synchronous loading
- Main use: server

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

- Slightly more complicated syntax, enabling AMD to work without eval() (or a compilation step).
- Designed for asynchronous loading
- Main use: browsers

```javascript
define(['jquery'] , function ($) {
    return function () {};
});
```

#### It is an improvement over CommonJS modules because:   
It works better in the browser, it has the least amount of gotchas. Other approaches have problems with debugging, cross-domain/CDN usage, file:// usage and the need for server-specific tooling.  
Defines a way to include multiple modules in one file. In CommonJS terms, the term for this is a "transport format", and that group has not agreed on a transport format.   
Allows setting a function as the return value. This is really useful for constructor functions. In CommonJS this is more awkward, always having to set a property on the exports object. Node supports module.exports = function () {}, but that is not part of a CommonJS spec.  

### ES 6 modules
The goal for ECMAScript 6 modules was to create a format that both users of CommonJS and of AMD are happy with:

- Similar to CommonJS, they have a compact syntax, a preference for single exports and support for cyclic dependencies.
- Similar to AMD, they have direct support for asynchronous loading and configurable module loading.

```javascript
    //------ lib.js ------
    export const sqrt = Math.sqrt;
    export function square(x) {
        return x * x;
    }
    export function diag(x, y) {
        return sqrt(square(x) + square(y));
    }
    
    //------ main.js ------
    import { square, diag } from 'lib';
    console.log(square(11)); // 121
    console.log(diag(4, 3)); // 5
```

#### Default exports (one per module)

##### CommonJS
```javascript
 //------ underscore.js ------
    var _ = function (obj) {
        ...
    };
    var each = _.each = _.forEach =
        function (obj, iterator, context) {
            ...
        };
    module.exports = _;
    
    //------ main.js ------
    var _ = require('underscore');
    var each = _.each;
    ...
```

##### ES 6 modules
```javascript
    //------ underscore.js ------
    export default function (obj) {
        ...
    };
    export function each(obj, iterator, context) {
        ...
    }
    export { each as forEach };
    
    //------ main.js ------
    import _, { each } from 'underscore';
    ...
```
#### Docs
- http://www.2ality.com/2014/09/es6-modules-final.html
