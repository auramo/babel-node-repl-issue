
# babel-node repl issue

babel-node repl works differently from compiled code + node regarding
import. The ES6-way of importing works fine when I compile code with
babel and run it with with the node binary. In babel-node I can't
seem to import a node-module. The import doesn't throw any error, but
when I try to use the module, I get ReferenceError. Details below.

First, run npm install. Then start the repl:

```
node_modules/.bin/babel-node
```

Now, try to make an ES6-import of our example lib (ramda):
```
import R from 'ramda'
R.identity(1)
```

This error occurs:
```
R.identity(1);
^
ReferenceError: R is not defined
```

However, direct call to CommonJS/Node require works:

```
const R = require('ramda')
R.identity(1)
-> 1
```

But when I do the same thing by compiling my ES6 code first, and then
run it with node, everything works fine:
```
node_modules/.bin/babel test-module.js --out-file test-module-compiled.js
node test-module-compiled.js
-> 1
```

I used node version v0.12.7.
