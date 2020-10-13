# node-addon-base

Boilerplate code for generating Node.js native addons.

To compile, run
```bash
npm install
cmake-js build
```

You can use the generated addon as follows.
```javascript
const addon = require('./build/Release/object-wrap-cmake-js');

const instance = new addon.ObjectWrapDemo('fry');
instance.greet('katie');
```
