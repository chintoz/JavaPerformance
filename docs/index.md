# Just In Time Compilation

## Displaying JIT information

JVM decides which part of the bytecode is going to be compiled. It is going to be decided based on the frequency of the method caslls. If a method is called frequently, then it is going to be compiled. This is called Just In Time Compilation.

They parameter to display information about compiled source code is `-XX:+PrintCompilation`.

```shell
    java -XX:+PrintCompilation MainClass
```

It will display information about the compiled source code. Here there is an example of the result of the execution of the command with this parameter.

```shell
    1       3       3       MainClass::main (1 bytes)
    4       3       3       MainClass::main @ 3 (1 bytes)
```

The meaning of the columns is the following: 
- The first column is the number of the compilation.
- The second column is the time in milliseconds since the JVM started.
- The third column is the time in milliseconds since the last compilation.
- The fourth column is the method that has been compiled.
- The fifth column is the size of the compiled code in bytes.
- The sixth column is the address of the compiled code. 

## JIT compilation levels

There are three levels of JIT compilation:

* **Client Compiler**: It is the default compiler. It is used for client applications. It is optimized for fast startup time and low memory footprint. It is enabled with the `-client` option.
* **Server Compiler**: It is used for server applications. It is optimized for high throughput. It is enabled with the `-server` option.
* **Tiered Compilation**: It is a combination of the client and server compilers. It is enabled with the `-tiered` option.

There is a way to disable tiered compilation with the `-XX:-TieredCompilation` option.

```shell
    java -XX:-TieredCompilation MainClass
```

To show deep information about compilation it could enabled VM diagnostic options and log compilation information. The following example shows how to enable the diagnostic options and log compilation information.

```shell
    java -XX:+UnlockDiagnosticVMOptions -XX:+LogCompilation MainClass
```

## JIT cache size   

The JIT cache size is the maximum size of the code cache. The code cache is the area where the compiled code is stored. The default value is 240 MB. It can be changed with the `-XX:ReservedCodeCacheSize` option.

```shell
    java -XX:ReservedCodeCacheSize=256m MainClass
```

There are other two parameters to configure code cache size that are `-XX:InitialCodeCacheSize` and `-XX:CodeCacheExpansionSize`. The first one is the initial size of the code cache and the second one is the size of the code cache expansion.