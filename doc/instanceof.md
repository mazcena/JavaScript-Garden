## The `instanceof` operator

The `instanceof` operator compares the constructors of its two operands. It is 
only useful when comparing custom made objects. Using it on built in types is
nearly as useless as the [typeof operator](#typeof).

### Comparing custom objects

    function Foo() {}
    function Bar() {}
    Bar.prototype = Foo;

    new Bar() instanceof Bar; // true
    new Bar() instanceof Foo; // false

### Using `instanceof` with native types

    new String('foo') instanceof String; // true
    new String('foo') instanceof Object; // true

    'foo' instanceof String; // false
    'foo' instanceof Object; // false

One important thing to note is that `instanceof` does of course not work on
objects that origin from different JavaScript contexts (e.g. different documents
in a web browser), since their constructors will not be the exact same object.

### In conclusion

The `instanceof` operator should **only** be used when dealing with custom made 
objects that origin from the same JavaScript context. Just like the
[`typeof`](#typeof) operator, every other use of it should be **avoided**.

