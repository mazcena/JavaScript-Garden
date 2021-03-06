## Objects

Everything in JavaScript acts like an object, with the only two exceptions being 
[`null`](#undefined) and [`undefined`](#undefined).

    false.toString() // 'false'
    [1, 2, 3].toString(); // '1,2,3'
    
    function Foo(){}
    Foo.bar = 1;
    Foo.bar; // 1

A common misconception is that number literals cannot be used as
objects. That is because a flaw in JavaScript's parser tries to parse the *dot 
notation* on a number as a floating point literal.

    2.toString(); // raises SyntaxError

There are a couple of workarounds which can be used in order make number 
literals act as object too.

    2..toString(); // the second point is correctly recognized
    2. toString(); // note the space
    (2).toString(); // 2 is evaluated first

### Objects as a data type

Objects in JavaScript can also be used as a [*Hashmap*][1], they mainly consist 
of named properties mapping to values.

Using the curly brace notation `{}` one can create a plain object. This new
object [inherits](#prototype) from `Object.prototype` and has no 
[own properties](#hasownproperty) defined on it.

    var foo = {}; // a new empty object

    // a new object with a property called 'test' with value 12
    var bar = {test: 12}; 

### Accessing properties

The properties of an object can be accessed in two ways, via either the dot
notation, or the square bracket notation.
    
    var foo = {name: 'Kitten'}
    foo.name; // kitten
    foo['name']; // kitten
    
    var get = 'name';
    foo[get]; // kitten
    
    foo.1234; // SyntaxError
    foo['1234']; // works

Both notations are identical in their workings, with the only difference being that
the square bracket notation allows for dynamic setting of properties, as well as
the use of property names that would otherwise lead to a syntax error.

### Deleting properties

The only way to actually remove a property from an object is to use the `delete`
operator; setting the property to `undefined` or `null` does **only** remove the
value associated with the property, but not the key.

    var obj = {
        bar: 1,
        foo: 2,
        baz: 3
    };
    obj.bar = undefined;
    obj.foo = null;
    delete obj.baz;

    for(var i in obj) {
        if (obj.hasOwnProperty(i)) {
            console.log(i, '' + obj[i]);
        }
    }

The above outputs both `bar undefined` and `foo null` - only `baz` got actually
removed and is therefore missing from the output.

### Notation of keys

    var test = {
        'case': 'I am a keyword so I must be notated as a string',
        delete: 'I am a keyword too so me' // raises SyntaxError
    };

Object properties can be both notated as plain characters and as strings. Due to
another mis-design in JavaScript's parser, prior to ECMAScript 5 the above will throw 
a `SyntaxError`.

This error arises from the fact that `delete` is a *keyword* of the language;
therefore, it must be notated as a string literal in order to ensure working
code under older JavaScript engines.

[1]: http://en.wikipedia.org/wiki/Hashmap