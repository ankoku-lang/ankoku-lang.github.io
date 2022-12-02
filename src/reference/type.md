# Type

Type is the type that specifies types. It's implemented in the VM, but is still totally meta.

## `type name(parent);`

Not a function, but built in syntax. Creates type `name` that inherits from `parent`.

### Example

```rust,ignore
type Cat(Object);
```
