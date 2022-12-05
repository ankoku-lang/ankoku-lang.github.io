# Function

Functions are instances of the Function class, which is an FFI class and private. They expose a few methods, generally for making more functions.

## `Function.call(this, arguments)`

Call this function with the specified arguments.

Implemented in the VM.

## `Function.bind(this, ...arguments)`

Bind this function with a starting number of parameters. Most commonly used to bind `this` in `Object.new`.

Example implementation:

```rust,ignore
fn Function.bind(this, ...arguments) {
	return fn(...args) {
		return this.call(arguments.concat(args));
	}
}
```
