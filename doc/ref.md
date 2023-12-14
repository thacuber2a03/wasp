# wasp's reference

wasp supports:
- numbers
- lists
- symbols
- strings
- `nil` and `t`

strings have no escaping whatsoever; this is being worked on, but as of now, no preprocessing is done on strings beforehand, including escaping double quotes.

comments start with `;`, and run to the end of the line.

## core forms

all core forms can be used as first class values; they're referred internally to as "corefuncs".
shadowing a corefunc is possible, but not really desirable, as you may completely lose the reference to that corefunc.
overwriting or making corefuncs is not possible.

- `(+ ...)`, `(- ...)`, `(* ...)`, `(/ ...)`

add, subtract, multiply, and divide all of their arguments left-to-right, respectively. division by zero is treated as an error.

- `(= a b)`

compares two objects. returns `t` if they're equal and `nil` otherwise.
corefuncs are compared by reference, while every other type is compared by value.

- `(< a b)`, `(<= a b)`

return `t` if `a` is numerically less than/less than or equal to `b`.

- `(or ...)`

evaluates each argument, and returns the first one that isn't `nil`; returns said argument and does not evaluate the rest. if no argument isn't `nil`, returns `nil`.

- `(and...)`

same as `or`, but returns `nil`. if any argument is `nil`. the last argument is returned if no argument is `nil`.

- `(not v)`

returns `nil` if val isn't `nil`, else `t`.

- `(quote v)` (alias `'v`)

returns `v` as is.

- `(eval v)` (alias `,v`)

evaluates `v`. this should probably be renamed.

- `(print ...)`

prints each of its arguments, separated by a space, and ends with a newline.

- `(list ...)`

compiles all it's arguments into a new list.

- `(do ...)`

begins a new environment, and evaluates each of it's arguments. returns the last one.

- `(if condition then ... else?)`

runs each `condition`, and if not `nil`, returns it's respective `then`. if no condition is met, returns `else`, if there is one.

```clojure
(set a 3)
(if
    (= a 1) (print "one")
    (= a 2) (print "two")
    (= a 3) (print "three")
    (print "idk")
)
; output: three
```

- `(while cond ...)`

evaluates each argument, as long as `cond` isn't `nil`.

- `(set sym v)`

tries to find and set `sym` in this environment. if it can't find it, searches all previous environments. if it still can't find it, binds `v` to `sym` in the current environment.

- `(def sym v)`

misleadingly named, binds `v` to `sym` in the global environment.
