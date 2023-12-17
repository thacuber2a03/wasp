# wasp's reference

wasp supports:
- numbers
- lists
- symbols
- strings
- functions
- macros
- `nil` and `t`

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

evaluates each argument, returns the first one that isn't `nil` and does not evaluate the rest. if all arguments are `nil`, returns `nil`.

- `(and ...)`

same as `or`, but returns `nil` if any argument is `nil`. the last argument is returned if no argument is `nil`.

- `(not v)`

returns `nil` if val isn't `nil`, else `t`.

- `(quote v)` (alias `'v`)

returns `v` as is.

- `(eval v)` (alias `,v`)

evaluates `v`.

- `(print ...)`

prints each of its arguments, separated by a space, and ends with a newline.

- `(list ...)`

compiles all it's arguments into a new list.

- `(do ...)`

begins a new environment, and evaluates each of it's arguments. returns the last one.

- `(func params ... & rest)`

makes and returns a "func".
unlike corefuncs, funcs' contents can be printed, and can store the value of the variables in the environment they're in for later use ("close over" them, closures).
the `rest` argument is a symbol that holds all extra arguments passed to the function.

- `(macro params ... & rest)`

makes and returns a "macro".
macros are like funcs, but their contents are evaluated *twice*, one to get the code to evaluate and another to actually evaluate it. this behavior allows metaprogramming, such as adding another way to declare funcs.

- `(if condition then ... else?)`

evaluates each `condition`, and if not `nil`, returns it's respective `then`. if no condition is met, returns `else`, if there is one.

```clojure
(set a 3)
(if
    (= a 1) (print "one")
    (= a 2) (print "two")
    (= a 3) (print "three")
    (print "idk")
)
; three
```

- `(while cond ...)`

repeatedly evaluates each argument, as long as `cond` isn't `nil`. returns last argument evaluated before the end of the loop.

- `(set sym val ...)`

tries to find and set `sym` in this environment. if it can't find it, searches all previous environments. if it still can't find it, binds `val` to `sym` in the current environment.
repeats for every other pair of `sym`s and `val`s there is.

```clojure
(set a 1 b 2 c (+ a b))
(print a b c) ; 1 2 3
```

- `(def sym val)`

misleadingly named, binds `val` to `sym` in the global environment.

- `(first list)`

returns the first item in a list.

- `(rest list)`

returns a new list with all the items that are after the first item in `list`.
returns `nil` if there's nothing after the first item.

- `(list? v)`

returns `t` if `v` is a list, and `nil` otherwise.

- `(length v)`

returns the length of a list or a string.

- `(cons v l)`

inserts `v` at the back of `l`.
if `l` is not a list, returns a list with both values inside.
if `l` is `nil`, returns a list with just `v` in it.

- `(concat a b)`

concatenates lists `a` and `b`.

- `(slice v a b)`

takes a subcopy of a list or a string from `a` to `b`.
negative indices are also accepted, with -1 being the value's end.
