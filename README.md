# wasp

so one day I was really bored and in my way to highschool I asked myself "what is the smallest human-readable LISP I can possibly make in one Lua file that has just enough constructs to make it turing-complete?"

this is what came out of that question, apparently

- check the [language reference](doc/ref.md)

## requirements

- Lua 5.4.6
- ...and that's about it

## todo

- [ ] implement functions and macros
- [ ] some more list manipulation functions
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
