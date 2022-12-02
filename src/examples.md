# Examples

Here are some basic examples to demonstrate the syntax and semantics.

## Hello World

```rust,ignore
print("Hello, world!");
```

## Recursive Fibonacci

```rust,ignore
fn fib(n) {
  if (n < 2) { n } else { fib(n - 1) + fib(n - 2) }
}
print("Hello, world!");
```

## First Class Functions

```rust,ignore
fn do_10_times(f) {
	for i in 0..10 {
		f(i);
	}
}

do_10_times(fn(i) {
	print(i)
});
```

## Objects

```rust,ignore
let object = {
	just_a: "A hashmap, dictionary, hash table, etc."
};

print(object.a_thing);
```

## Classes

For more about OOP, read [Object Oriented Programming in Ankoku](./oop.md).

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

let cow = Cow.new();

cow.make_sound(); // Mooo
let animal = Animal.new();

Animal.make_sound(); // Animals.
```
