# How Code Execute ?

# Compile

-javac Main.java

### Parse

### - Java Code

![](img/hello_world.png)

### - Tokens (Lexical Analysis)

The compiler scans the code and, using grammar rules, turns characters into tokens.
Whitespace is mostly ignored — but it is NOT the main rule.

### - Abstract syntax tree (Parse)(AST)

Convert Tokens to AST

![](img/ASTree.png)

### - Optimize

- There are optimizations done by the Java compiler (javac) and optimizations done later by the JVM (JIT).
- Now we talk about javac

### Basic rules

---
- Constant folding
``` Java
int x = 3 << 2;
 ```
in bytecode we recive
``` Java
int x = 12;
 ```
 --- 

-  Inlining constants    
   then in the bytecode, the compiler usually puts the value 10 directly, instead of generating a lookup like A.SIZE.
``` Java
class A {
    static final int SIZE = 10;
}
int x = A.SIZE;
 ```
in vm we see 
``` Java
int x = 10;
 ```
 ---
- Removing unreachable code  
If the compiler sees code that can never run, it may remove it.
``` Java
if (false) {
System.out.println("never");
}
 ```
in bytecode we se nothing

--- 

-  Pre Calculate
``` Java
int x = 10;
int y = 5;
int res = x + y;
 ```
in bytecode we get 
``` Java
int res = 15;
 ```
# Execute
