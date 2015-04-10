# make-error

[![Build Status](https://img.shields.io/travis/julien-f/js-make-error/master.svg)](http://travis-ci.org/julien-f/js-make-error)
[![Dependency Status](https://david-dm.org/julien-f/js-make-error/status.svg?theme=shields.io)](https://david-dm.org/julien-f/js-make-error)
[![devDependency Status](https://david-dm.org/julien-f/js-make-error/dev-status.svg?theme=shields.io)](https://david-dm.org/julien-f/js-make-error#info=devDependencies)

> Make your own error types!


## Features

- Compatible Node & browsers
- `instanceof` support
- `error.name` & `error.stack` support

## Installation

### Node & Browserify

Installation of the [npm package](https://npmjs.org/package/make-error):

```
> npm install --save make-error
```

Then require the package:

```javascript
var makeError = require('make-error');
```

### Browser

Clone the git repository and compile the browser version of the
library:

```
> git clone https://github.com/julien-f/js-make-error.git
> npm install
> npm run browserify
```

Then import the script `make-error.js` which has been compiled in the
`dist/` directory:

```html
<script src="make-error.js"></script>
```

## Usage

### Basic named error

```javascript
var CustomError = makeError('CustomError');

// Parameters are forwarded to the super class (here Error).
throw new CustomError('a message');
```

### Advanced error class

```javascript
function CustomError(customValue) {
  CustomError.super.call(this, 'custom error message');

  this.customValue = customValue;
}
makeError(CustomError);

// Feel free to extend the prototype.
CustomError.prototype.myMethod = function CustomError$myMethod() {
  console.log('CustomError.myMethod (%s, %s)', this.code, this.message);
};

//-----

try {
  throw new CustomError(42);
} catch (error) {
  error.myMethod();
}
```

### Specialized error

```js
var SpecializedError = makeError('SpecializedError', CustomError);

throw new SpecializedError(42);
```

## Contributions

Contributions are *very* welcomed, either on the documentation or on
the code.

You may:

- report any [issue](https://github.com/julien-f/js-make-error/issues)
  you've encountered;
- fork and create a pull request.

## License

ISC © [Julien Fontanet](http://julien.isonoe.net)
