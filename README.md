# clox : lox in c, compiler, byte-code, and virtual machine

## [simple build](https://craftinginterpreters.com/chunks-of-bytecode.html)

* AST walk or not

| AST | no AST |
| --- | ------ |
| simple to implement: the runtime representation of code is mapped directly to the syntax | memory-efficiency |
| portable but slow | no overhead of each AST node |

So in between AST and machine code, there is a bytecode.
 
```
$ gcc src/main.c src/chunk.c src/memory.c src/debug.c -o test 
$./test 
== test chunk ==
0000 OP_RETURN
```

## reference

* https://craftinginterpreters.com/chunks-of-bytecode.html

