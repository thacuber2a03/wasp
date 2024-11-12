# wasp

so one day I was really bored and in my way to highschool I asked myself "what is the smallest human-readable LISP I can possibly make in one Lua file that has enough constructs to make it nice to use and be turing-complete?"

this is what came out of that question, apparently

---

- [language reference](doc/ref.md)

## requirements

- Lua 5.4.6
- ...and that's about it

## todo

- [x] implement functions and macros
- [ ] more list manipulation functions
- [ ] more string manipulation functions
- [ ] make it ***smaller***

## running

passing an argument to the interpreter before running it will make it try to open it as a file and read from it

### *nix systems:
just run the file as if it was an executable:
```
wasp
```

### basically everthing else:
run it through Lua interpreter:
```
lua wasp
```

## extra
this project is licensed under the [MIT license](LICENSE). contributions are welcome, as long as they add something of value and/or are worth it.
