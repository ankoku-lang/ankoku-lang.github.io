## Object Oriented Programming in Ankoku

OOP is implemented into Ankoku, in a mix of prototypal and traditional styles, with the goals of being fast without too much magic. When defining a class, you define all the methods like this:

```rust,ignore
class Animal {
	fn make_sound() {
		print("*crickets*");
	}
}

class Cow: Animal {
	fn make_sound() {
		if (this.loud) {
			print("MOOOO!!");
		} else {
			print("Mooo");
		}
	}
}
```

but they actually desugar into normal functions:

```rust,ignore
fn Animal.make_sound(this) {
	print("*crickets*");
}

fn Cow.make_sound(this) {
	if (this.loud) {
		print("MOOOO!!");
	} else {
		print("Mooo");
	}
}
```

(`this` is prepended as the first argument unless the function is a `static fn`)

And then it also creates constructor functions and a [type](./reference/type.md):

```rust,ignore
type Animal(Object);

fn Animal.new() {
	// user code goes here...
	Object.new(Animal) // create a new object of type Animal
}

type Cow(Animal);

fn Cow.new() {
	Object.new(Cow) // create a new object of type Cow
}
```

[Object](./reference/object.md) is at the top of the inheritance hierarchy and includes static methods to create new objects.

Anyways, each object has a type:

```rust,ignore
let object = {}; // empty object, desugars to Object.new(Object)

print(object is Object); // true

let animal = Object.new(Animal); // animal

print(animal is Animal); // true
```

The type is accessible by calling `typeof`:

```rust,ignore
let object = {}; // empty object

print(typeof(object) == Object); // true
print(typeof(object) == Animal); // false

let animal = Object.new(Animal); // animal

print(typeof(object) == Animal); // true
print(typeof(animal) == Object); // false
```

However, `typeof` only gives the direct type, so use `is` for comparisons to allow inherited types.

Anyways, `Object.new(type)` will set properties on the object to the associated non-static functions (`fn Animal.*`):

```rust,ignore
let animal = Object.new(Animal); // finds all functions for animal (Animal.*)

print(animal.make_sound); // [function]
print(animal); // { make_sound: [function] }
```

But it will set it to bound versions of them (using `.bind` on [Function](reference/function.md)), so the first parameter (`this`) is set to the created object.

```rust,ignore
type Example(Object);
fn Example.assoc_types(this) {
	return this;
}

let example = Object.new(Example);

print(example.assoc_types() == example); // true
```

And you can call associated functions yourself as well, if you'd like to use a specific version:

```rust,ignore
let cow = Cow.new();

Animal.make_sound(cow); // prints "*crickets*"
```

This is a reasonably elegant system that is sort of confusing, but combines some of the dynamicity of prototypes with the rigidity of OOP.
