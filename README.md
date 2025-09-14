# clox : lox in c, compiler, byte-code, and virtual machine

## [ch14. chunks of bytecode](https://craftinginterpreters.com/chunks-of-bytecode.html)

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
0000  123 OP_CONSTANT         0 '1.2'
0002 OP_RETURN
```

## [ch15. a virtual machine](https://craftinginterpreters.com/a-virtual-machine.html)

```
$ gcc src/main.c src/chunk.c src/memory.c src/debug.c src/value.c src/vm.c -o test
$./test 
== test chunk ==
0000  123 OP_CONSTANT         0 '1.2'
0002    | OP_NEGATE
0003    | OP_RETURN
          
0000  123 OP_CONSTANT         0 '1.2'
          [ 1.2 ]
0002    | OP_NEGATE
          [ -1.2 ]
0003    | OP_RETURN
-1.2
```

* add binary operations

```
$ gcc src/main.c src/chunk.c src/memory.c src/debug.c src/value.c src/vm.c -o test
$./test 
== test chunk ==
0000  123 OP_CONSTANT         0 '1.2'
0002    | OP_CONSTANT         1 '3.4'
0004    | OP_ADD
0005    | OP_CONSTANT         2 '5.6'
0007    | OP_DIV
0008    | OP_NEGATE
0009    | OP_RETURN
          
0000  123 OP_CONSTANT         0 '1.2'
          [ 1.2 ]
0002    | OP_CONSTANT         1 '3.4'
          [ 1.2 ][ 3.4 ]
0004    | OP_ADD
          [ 4.6 ]
0005    | OP_CONSTANT         2 '5.6'
          [ 4.6 ][ 5.6 ]
0007    | OP_DIV
          [ 0.821429 ]
0008    | OP_NEGATE
          [ -0.821429 ]
0009    | OP_RETURN
-0.821429
```

## cmake

```
$ mkdir build && cd build
$ cmake .. && make
$ ./clox
```

## [ch 16. Scanner](https://craftinginterpreters.com/scanning-on-demand.html)

source --> scanner --> tokens --> compiler --> bytecode chunks --> vm

## [ch 17. compiler](https://craftinginterpreters.com/compiling-expressions.html)

```
$ cd build && cmake .. && make
$./clox 
> 3+2
== code ==
0000    1 OP_CONSTANT         0 '3'
0002    | OP_CONSTANT         1 '2'
0004    | OP_ADD
0005    2 OP_RETURN
          
0000    1 OP_CONSTANT         0 '3'
          [ 3 ]
0002    | OP_CONSTANT         1 '2'
          [ 3 ][ 2 ]
0004    | OP_ADD
          [ 5 ]
0005    2 OP_RETURN
5
> 
```

## [ch 18. types of values](https://craftinginterpreters.com/types-of-values.html)

* how do we represent the type of a value?

* how do we store the value itself? 

```
$./clox
> true
== code ==
0000    1 OP_TRUE
0001    2 OP_RETURN
          
0000    1 OP_TRUE
          [ true ]
0001    2 OP_RETURN
true
> 
```

## [ch. 19 strings](https://craftinginterpreters.com/strings.html)

strings have varied length for storage in heap. Other smaller are in the stack.


## reference

* https://craftinginterpreters.com/chunks-of-bytecode.html

* [the implementation of Lua 5.0 PDF](https://www.lua.org/doc/jucs05.pdf)

