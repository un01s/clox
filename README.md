# clox : lox in c, compiler, byte-code, and virtual machine

## [chunks of bytecode](https://craftinginterpreters.com/chunks-of-bytecode.html)

* AST walk or not

| AST | no AST |
| --- | ------ |
| simple to implement (runtime rep of code mapped directly to the syntax) | memory-efficiency |
| portable but slow | no overhead of each AST node |

So in between AST and machine code, there is a bytecode.
 
```
$ gcc src/main.c src/chunk.c src/memory.c src/debug.c src/value.c -o test
$./test 
== test chunk ==
0000 OP_CONSTANT         0 '1.2'
0002 OP_RETURN
```

## reference

* https://craftinginterpreters.com/chunks-of-bytecode.html

